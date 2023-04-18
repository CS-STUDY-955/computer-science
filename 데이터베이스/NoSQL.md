# NoSQL
## NoSQL이란?
- Not Only SQL
- Non-Relational Database
- 스키마도 없고, 관계도 없음
- 여러 데이터 모델(key-value, document, graph, ...)로 데이터를 저장함

## SQL vs NoSQL

|        | SQL    | MySQL        |
|--------|--------|--------------|
| 데이터 단위 | table  | various      |
| 조인     | 존재     | 존재하지 않음      |
| 확장     | 수직적    | 수평적          |
| 유연성    | 덜 유연함  | 유연함          |
| 무결성    | 무결성 보장 | 데이터 중복 처리 필요 |

## 선택 가이드
- 관계를 맺고 있는 데이터가 자주 변경되는 경우: SQL
- 명확한 스키마가 사용자와 데이터에게 중요한 경우: SQL
- 정확한 데이터 구조를 알 수 없는 경우: NoSQL
- 연산이 읽기 위주로 발생하며, 변경이 자주 없는 경우: NoSQL
- 막대한 양의 데이터를 다뤄 수평적 확장이 필요한 경우: NoSQL

## 대표 NoSQL 서비스
1. MongoDB
   - Document-oriented 데이터베이스
   - JSON과 유사한 BSON(Binary JSON) 형식으로 데이터를 저장
   - 수평 확장이 용이하고 복제 기능도 제공
```mongodb-json
{
   "product_id": "001",
   "product_name": "Apple iPhone 13",
   "category": "Mobile Phones",
   "price": 1099.00,
   "colors": ["White", "Black", "Blue", "Red"],
   "specs": {
      "display": "6.1 inches, 1170 x 2532 pixels",
      "camera": "12 MP, f/1.6, 26mm (wide), 1.7µm, dual pixel PDAF, sensor-shift OIS",
      "battery": "Non-removable Li-Ion 3200 mAh battery"
   }
}
```

2. Redis
   - In-memory 데이터 구조 저장소
   - 데이터를 메모리에 저장하여 빠른 속도를 보장
   - 캐싱, 세션 관리, 메시지 브로커 등으로 사용
```redis
{
   "product_id_001": "{\"product_name\":\"iPhone 13 Pro Max\",\"category\":\"Smartphones\",\"price\":1099.99,\"colors\":[\"Graphite\",\"Gold\",\"Silver\",\"Sierra Blue\"],\"specs\":{\"display\":\"6.7 inches, Super Retina XDR OLED, 120Hz, HDR10, Dolby Vision\",\"processor\":\"A15 Bionic, 5-nanometer process\",\"camera\":\"12 MP, f/1.5, 26mm (wide), 12 MP, f/2.8, 77mm (telephoto), 12 MP, f/1.8, 13mm (ultrawide), TOF 3D LiDAR scanner (depth)\",\"battery\":\"Li-Ion 4352 mAh, non-removable\"}}",
   "product_id_002": "{\"product_name\":\"Samsung Galaxy S22 Ultra 5G\",\"category\":\"Smartphones\",\"price\":1299.99,\"colors\":[\"Phantom Black\",\"Phantom Silver\",\"Phantom Titanium\"],\"specs\":{\"display\":\"6.8 inches, Dynamic AMOLED 2X, 120Hz, HDR10+, Gorilla Glass Victus\",\"processor\":\"Exynos 2200, 5-nanometer process\",\"camera\":\"108 MP, f/1.8, 24mm (wide), 10 MP, f/4.9, 240mm (periscope telephoto), 10 MP, f/2.2, 16mm (ultrawide), 2 MP, f/2.4, (macro)\",\"battery\":\"Li-Po 5000 mAh, non-removable\"}}",
   "product_id_003": "{\"product_name\":\"Sony WH-1000XM4\",\"category\":\"Headphones\",\"price\":349.99,\"colors\":[\"Black\",\"Silver\"],\"specs\":{\"type\":\"Over-Ear Wireless Headphones\",\"noise_cancellation\":\"Yes, HD Noise Cancelling Processor QN1, Dual Noise Sensor Technology\",\"battery\":\"30 Hours Battery Life\"}}"
}
```

3. DynamoDB
   - 키-값 데이터 모델을 사용하는 NoSQL 데이터베이스
   - AWS에서 제공하는 서비스
   - 높은 확장성과 가용성, 빠른 성능을 제공
```json
{
  "id": "user1234",
  "name": "John Smith",
  "email": "john.smith@example.com",
  "join_date": "2022-04-18"
}
```

## Spring에서 MongoDB를 사용하는 예시 코드
```java
// MongoDB Java Driver를 사용하여 MongoDB 데이터베이스에 접속하는 예시 코드
public class MongoDBExample {

    public static void main(String[] args) {
        // MongoDB 서버에 접속
        MongoClient mongoClient = new MongoClient("localhost", 27017);
        
        // 데이터베이스 선택
        MongoDatabase database = mongoClient.getDatabase("test");
        
        // 데이터베이스에 컬렉션 생성
        database.createCollection("users");
    }
}
```
```java
// Spring Data MongoDB를 사용하여 MongoDB 데이터베이스에 데이터를 저장하는 예시 코드
@Component
public class MongoDBExample {
    
    @Autowired
    private MongoTemplate mongoTemplate;
    
    public void saveUser(User user) {
        // MongoDB에 User 객체 저장
        mongoTemplate.save(user);
    }
}
```