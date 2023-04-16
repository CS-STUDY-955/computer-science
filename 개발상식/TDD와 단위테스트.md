# TDD와 단위테스트
## TDD란?
- Test-Driven Development
- SW 개발 방법론 중 하나
- 테스트를 먼저 작성하고 그에 맞는 코드를 개발하는 방법

## TDD 진행 과정
1. 테스트 케이스 작성
2. 테스트 실행 및 실패 확인
3. 코드 작성
4. 코드 리팩토링
5. 테스트 실행 및 성공 확인

```java
public class MemberServiceTest {

    MemberService memberService;

    @BeforeEach
    public void beforeEach() {
        memberService = new MemberService();
    }

    @Test
    void 회원가입() {
        // given
        Member member = new Member();
        member.setName("hello");

        // when
        Long saveId = memberService.join(member);

        // then
        Member findMember = memberService.findOne(saveId).get();
        assertThat(member.getName()).isEqualTo(findMember.getName());
    }
}
```
```java
@Service
@Transactional
public class MemberService {

    private final MemberRepository memberRepository;

    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    public Long join(Member member) {
        validateDuplicateMember(member);
        memberRepository.save(member);
        return member.getId();
    }

    private void validateDuplicateMember(Member member) {
        memberRepository.findByName(member.getName())
                .ifPresent(m -> {
                    throw new IllegalStateException("이미 존재하는 회원입니다.");
                });
    }

    public Optional<Member> findOne(Long memberId) {
        return memberRepository.findById(memberId);
    }

    public List<Member> findMembers() {
        return memberRepository.findAll();
    }
}

```
```java
@SpringBootTest
@Transactional
class MemberRepositoryTest {

    @Autowired
    private MemberRepository memberRepository;

    @Test
    public void testFindByAgeGreaterThan() {
        // Given
        Member member1 = new Member("John", 25);
        Member member2 = new Member("Mike", 30);
        Member member3 = new Member("Jane", 35);
        memberRepository.saveAll(Arrays.asList(member1, member2, member3));

        // When
        List<Member> members = memberRepository.findByAgeGreaterThan(30);

        // Then
        assertThat(members.size()).isEqualTo(2);
        assertThat(members.get(0).getName()).isEqualTo("Mike");
        assertThat(members.get(1).getName()).isEqualTo("Jane");
    }
}
```
```java
public interface MemberRepository extends JpaRepository<Member, Long> {
    List<Member> findByAgeGreaterThan(int age);
}
```
## 테스트의 장점
- 변화에 대한 두려움을 줄여주어 리팩토링이 편함
- 디버깅 시간을 줄여줌
- 동작하는 문서 역할을 함

## TDD 장점
- 테스트된 코드의 비율을 나타내는 **테스트 커버리지**가 높아짐
- 요구사항 이상으로 개발하는 **오버엔지니어링** 방지
- 설계에 대한 피드백이 빠름

## TDD 주의사항
- 인터페이스에 대해 테스트 케이스를 작성해야함

## 단위테스트란?
- 가장 작은 단위의 테스트
- 일반적으로 메서드 레벨
- 테스트 케이스를 작성하는 절차 및 프로세스를 의미

## 단위테스트의 목적
- 문제점 조기 발견
- 쉬운 변경
- 품질 향상
- 코드의 문서화

## 단위테스트의 FIRST 법칙
- FAST: 테스트는 빠르게 동작해야 함
- Independent: 테스트는 다른 테스트에 독립적이어야 함
- Repeatable: 테스트는 어떠한 환경에서도 반복가능해야 함
- Self-Validating: 테스트는 성공과 실패를 리턴해야 함
- Timely: 테스트 코드는 실제 코드를 구현하기 전에 구현해야 함

```java
@RunWith(MockitoJUnitRunner.class)
public class MemberServiceTest {
    
    @Mock
    private MemberRepository memberRepository;

    @InjectMocks
    private MemberService memberService;

    @Test
    public void testGetMemberById() {
        Long memberId = 1L;
        Member member = new Member();
        member.setId(memberId);
        member.setName("John Doe");
        member.setEmail("john.doe@example.com");
        when(memberRepository.findById(memberId)).thenReturn(Optional.of(member));
        MemberDto result = memberService.getMemberById(memberId);
        assertEquals(memberId, result.getId());
        assertEquals(member.getName(), result.getName());
        assertEquals(member.getEmail(), result.getEmail());
    }

    @Test
    public void testCreateMember() {
        MemberDto memberDto = new MemberDto();
        memberDto.setName("Jane Doe");
        memberDto.setEmail("jane.doe@example.com");
        Member member = new Member();
        member.setId(1L);
        member.setName(memberDto.getName());
        member.setEmail(memberDto.getEmail());
        when(memberRepository.save(any(Member.class))).thenReturn(member);
        MemberDto result = memberService.createMember(memberDto);
        assertEquals(member.getId(), result.getId());
        assertEquals(member.getName(), result.getName());
        assertEquals(member.getEmail(), result.getEmail());
    }
}
```
```java
@RunWith(SpringRunner.class)
@WebMvcTest(MemberController.class)
public class MemberControllerUnitTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private MemberService memberService;

    @MockBean
    private MemberRepository memberRepository;

    @Test
    public void testGetAllMembers() throws Exception {
        // given
        List<Member> members = new ArrayList<>();
        members.add(new Member(1L, "John", "Doe"));
        members.add(new Member(2L, "Jane", "Doe"));
        given(memberService.getAllMembers()).willReturn(members);

        // when + then
        mockMvc.perform(get("/members"))
                .andExpect(status().isOk())
                .andExpect(content().contentType(MediaType.APPLICATION_JSON))
                .andExpect(jsonPath("$", hasSize(2)))
                .andExpect(jsonPath("$[0].id", is(1)))
                .andExpect(jsonPath("$[0].firstName", is("John")))
                .andExpect(jsonPath("$[0].lastName", is("Doe")))
                .andExpect(jsonPath("$[1].id", is(2)))
                .andExpect(jsonPath("$[1].firstName", is("Jane")))
                .andExpect(jsonPath("$[1].lastName", is("Doe")));
    }

    @Test
    public void testGetMemberById() throws Exception {
        // given
        Member member = new Member(1L, "John", "Doe");
        given(memberService.getMemberById(1L)).willReturn(member);

        // when + then
        mockMvc.perform(get("/members/1"))
                .andExpect(status().isOk())
                .andExpect(content().contentType(MediaType.APPLICATION_JSON))
                .andExpect(jsonPath("$.id", is(1)))
                .andExpect(jsonPath("$.firstName", is("John")))
                .andExpect(jsonPath("$.lastName", is("Doe")));
    }
}
```