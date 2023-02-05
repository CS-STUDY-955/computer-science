# 데이터와 XML parsing
## 데이터의 종류
- CVS: Comma separated Value
  - ','로 데이터를 구분함
  - 용량이 작지만, 뭐가 무슨 데이터를 뜻하는지 알지 못함

```cvs
id, 이름, 전공
1, 김철수, 기계공학과
2, 봉미선, 수학과
3, 신짱구, 아동교육과
```

- XML: Extensible markup language
  - HTML과 비슷하게 태그를 기반으로 데이터를 저장
    - 단, 사용자가 직접 태그를 만들 수 있음
  - 구조적이지만 정확한 문법이 필요하고, 용량이 큼

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<dataGrid>
    <records>
        <record>
            <name>만리포 관광지</name>
            <type>관광지</type>
            <address class="충청도">충청남도 태안군 소원면 만리포2길 190-3</address>
            <test>12</test>
            <Test>15</Test>
        </record>
    </records>
<dataGrid>
```

- JSON: Javascript object notation
  - 자바스크립트식 객체 표현이라는 뜻이지만, 다른 언어들과도 호환됨
  - 구조를 가지며 객체로 표현
```json
 {
    "이름": "홍길동",
    "나이": 55,
    "성별": "남",
    "주소": "서울특별시 양천구 목동",
    "특기": ["검술", "코딩"],
    "가족관계": {"#": 2, "아버지": "홍판서", "어머니": "춘섬"},
    "회사": "경기 수원시 팔달구 우만동"
 }
```

## XML
### 기본 문법
1. 반드시 시작이 정해짐
2. 반드시 root element가 존재해야 함(나머지 태그들은 tree의 형태로 구성됨)
1. 시작태그와 종료 태그가 일치 해야함
2. 시작 태그는 key-value 구조의 속성을 가질 수 있음
3. 태그는 대소문자를 구별함

## Parsing
- 문서에서 필요한 정보를 얻기 위해 태그를 구별하고 내용을 추출하는 과정

### SAX parser: Simple API for XML parser
  - 문서를 읽으며 태그의 시작, 종료 등 이벤트 기반으로 처리하는 방식
  - 읽기만 하는데엔 속도가 빠르지만, 데이터를 읽고난 뒤, 수행하는 작업들에는 적합하지 않음
  
#### SAX의 예시
  - Handler
```java
// 엘리먼트의 시작을 탐지
@Override
public void startElement(String uri, String localName, String qName, Attributes att) {
  temp = "";
  if (qName.equals("record")) {
    tripDto = new TripDto(num++);
  }
}

// 엘리먼트 안의 내용을 저장
@Override
public void characters(char[] ch, int start, int length) {
  temp = new String(ch, start, length);
}

// 엘리먼트의 종료 태그를 감지하면, 그 내용을 저장
@Override
public void endElement(String uri, String localName, String qName) {
  if (qName.equals("관광지명")) {
    tripDto.setTouristDestination(temp);
  } else if (qName.equals("소재지도로명주소")) {
    tripDto.setStreetAddress(temp);
  } else if (qName.equals("소재지지번주소")) {
    tripDto.setLotAddress(temp);
  } else if (qName.equals("record")) {
    trips.add(tripDto);
  }
}
```
  - Parser
``` java
SAXParserFactory factory = SAXParserFactory.newInstance();

String tripInfoFilePath = "res/전국관광지정보표준데이터.xml";

try {
  SAXParser parser = factory.newSAXParser();
  TouristDestinationSAXHandler handler = new TouristDestinationSAXHandler();
  parser.parse(tripInfoFilePath, handler);
  tripInfo = handler.getTrips();

  size = tripInfo.size();
} catch (Exception e) {
  e.printStackTrace();
}
```


### DOM parser: Document Object Model
  - 문서를 다 읽고 난 뒤, 문서의 구조 전체를 자료구조에 저장하며 탐색
  - 자료구조에 데이터 전체를 저장하므로 여러 작업들을 수행하는데엔 편하지만, 탐색 자체는 무거움

#### DOM의 예시
- 대상 파일
```XML
<class name="test">
  <teacher name="t1"/>
  <teacher name="t2"/>
  <student name="s1">
    <ID num="1"/>
    <major>수학</major>
  <student/>
  <student name="s2">
    <ID num="2"/>
    <major>기계공학</major>
  </student>
</class>
```
- parser
```java
// XML 문서 파싱
DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
DocumentBuilder documentBuilder = factory.newDocumentBuilder();
Document document = documentBuilder.parse("sample.xml");

// root 구하기
Element root = document.getDocumentElement();

// root의 속성
System.out.println("class name: " + root.getAttribute("name"));

NodeList childeren = root.getChildNodes(); // 자식 노드 목록 get
for(int i = 0; i < childeren.getLength(); i++){
  Node node = childeren.item(i);
  if(node.getNodeType() == Node.ELEMENT_NODE){ // 해당 노드의 종류 판정(Element일 때)
    Element ele = (Element)node;
    String nodeName = ele.getNodeName();
    System.out.println("node name: " + nodeName);
    if(nodeName.equals("teacher")){
      System.out.println("node attribute: " + ele.getAttribute("name"));
    }
    else if(nodeName.equals("student")){
      // 이름이 student인 노드는 자식노드가 더 존재함
      NodeList childeren2 = ele.getChildNodes();
      for(int a = 0; a < childeren2.getLength(); a++){
        Node node2 = childeren2.item(a);
        if(node2.getNodeType() == Node.ELEMENT_NODE){
          Element ele2 = (Element)node2;
          String nodeName2 = ele2.getNodeName();
          System.out.println("node name2: " + nodeName2);
          System.out.println("node attribute2: " + ele2.getAttribute("num"));
        }
        if(node.getNodeType() == Node.ELEMENT_NODE){
          Element ele2 = (Element)node2;
          System.out.println(ele2.getTextContent());
        }
      }
    }
  }
}
```

===============================================

참고문헌
- https://blog.naver.com/qbxlvnf11/221324667993
