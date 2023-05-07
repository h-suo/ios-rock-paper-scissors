# 묵찌빠 게임 :fist: :v: :raised_hand: 

> **콘솔을 통해 게임을 진행하며 최초 실행시** 
"가위(1), 바위(2), 보(3)! <종료 : 0> : "를  출력하고, 사용자에게 0,1,2,3중 한 가지를 입력 받아 결과에 따라 게임을 이어가는 게임입니다.
    - 가위, 바위, 보를 비긴 경우 :  다시 가위, 바위, 보 게임 진행합니다.
    - 가위, 바위, 보 게임에서 승패가 갈리 경우 : 묵찌빠로 이어서 게임을 진행합니다.

</br>

## 목차

1. [팀원](#1.)
2. [순서도](#2.)
3. [타임라인](#3.)
4. [실행 화면(기능 설명)](#4.)
5. [트러블 슈팅](#5.)
6. [참고 링크](#6.)
7. [팀 회고](#7.)
---

</br>

<a id="1."></a>
## 1. 팀원
| [Erick](https://github.com/h-suo)  | [Karen 🐕](https://github.com/karenyang835) |
| :--------: | :--------: |
| <img src="https://user-images.githubusercontent.com/109963294/235300758-fe15d3c5-e312-41dd-a9dd-d61e0ab354cf.png" height="150"/>| <Img src="https://i.imgur.com/auFOXpc.png" width="150"/>| 

---
<a id="2."></a>

</br>

## 2. 순서도

<details>
<summary>펼쳐보기</summary>
    
![](https://i.imgur.com/YMukIPx.png)
    
</details>

--- 

</br>

<a id="3."></a>
## 3. 타임라인

### 2023.05.01.(월)
<img src="https://i.imgur.com/zA6caJM.png" height="16"/> **가위바위보 게임 구현**
- 열거형 타입 추가 (가위, 바위, 보)
- 게임의 승패 여부 확인 함수 정의
- 사용자 입력 함수 정의

<img src="https://i.imgur.com/JwTMWid.png" height="16"/>

- 2중 들여쓰기 문제를 해결하기 위해 함수 2개로 분리
- `getUserInput()`안에 있던 `while`문을 분리해서 `startGame()`를 새롭게 정의
- `playingGame()` 삭제
- `getUserInput`안에 있는 `While`문을 옮겨서 `startGame()`를 정의


### **2023.05.02.(화)**
<img src="https://i.imgur.com/JwTMWid.png" height="16"/> **Pull requests 확인 후 수정**
- `getUserInput()`안의 `guard`문 조건 병합
- `compareRockPaperScissors()` `switch`구문 튜플로 전환
- `getUserInput()`함수를 기능 분리
- `getUserInput`는 입력값받는 것
- `checkUserInput`에 입력값과 조건을 검사하는 기능으로 새롭게 정의
- `compareRockPaperScissors()` 함수의 리턴값 `String` -> `Bool`
- `isGameOver`을 생성하여 게임이 이기고 졌을 때만 게임이 종료되도록 변경

### **2023.05.04.(목)**
<img src="https://i.imgur.com/JwTMWid.png" height="16"/>  **묵찌빠 게임 구현**
- `RockPaperScissorsgame`, `MukjippaGame` 구조체 생성
    - `MukjippaGame` 내부에 순서를 알려주는 `turn`을 추가
    - `MukjippaGame` 내에 `compare`함수를 `Mukjippa` 룰에 맞게 수정
- `RockPaperScissors` 열거형을 토대로 `Mukjippa`열거형 생성
- 게임의 결과 나타내는 `GameResult` 열거형 생성
- `RockPaperScissorsGame` 내 `startGame`이 `GameResult`를 리턴하도록 변경
- `MukjippaGame`에서 `checkRockPaperScissorsGameResult`를 이용해 `GameResult`를 받아 `turn`으로 할당

<img src="https://i.imgur.com/JwTMWid.png" height="16"/>

- `RockPaperScissors` 열거형의 원시값을 `String`으로 바꿔 `String` -> `Int` 타입 변환 코드를 제거
- `gameOver` 상수를 만들어 `case` "0"을 `gameOver`로 명시
- 기존 생성한 열거형들을 `Type`로 병합
- 중복 되어지는 `Bool` 값을 `isGameInProgress` 구조체의 인스턴스로 병합


### **2023.05.05.(금)**
- `README` 작성
- 순서도 작성

---

</br>

<a id="4."></a>
## 4. 실행 화면(기능 설명)

| 게임 종료시 | 잘못된 입력 | 
| :--------: | :--------: |
| <Img src = "https://i.imgur.com/YxGMULh.gif" width="350"/> | <Img src = "https://i.imgur.com/lPnr4DV.gif" width="350"/> |

| 비겼을 때 가위바위보 다시 실행 | 가위바위보 승리 후 묵찌빠 실행 | 
| :--------: | :--------: |
| <Img src = "https://i.imgur.com/aW86Yi2.gif" width="350"/> | <Img src = "https://i.imgur.com/fYQT0mg.gif" width="350"/> |

---

</br>

<a id="5."></a>
## 5. 트러블 슈팅
### 🔥 코드 들여쓰기 2번 초과하는 문제점
- `while`와 `if`문을 중첩해서 사용하다 보니 2중 들여쓰기가 되어서 제약 사항에 `while`문을 `stareGame`함수 안에 구현하는 방식으로 수정하여 해결했습니다.

<details>
<summary>세부 사항</summary>

#### 수정 전
```swift
func getRockPaperScissors() {
    while true {
        print("가위(1), 바위(2), 보(3)! <종료 : 0> :", terminator: " ")
        if let input = readLine(), let choice = Int(input) {
            if choice == 0 {
                print("게임 종료")
                break
            } else if choice < 1 || choice > 3 {
                print("잘못된 입력입니다. 다시 시도해주세요.")
                continue
            }
        }
    }
}
```

#### 수정 후
```swift
func getUserInput() -> Bool {
    var isUserSelect: Bool = true

    print("가위(1), 바위(2), 보(3)! <종료 : 0> :", terminator: " ")
    guard let input = readLine() else { return isUserSelect }

    switch input {
    case "1", "2", "3":
        guard let inputNumber = Int(input) else { return isUserSelect }
        guard let playerRockPaperScissors = RockPaperScissors(rawValue: inputNumber) else { return isUserSelect }
        guard let randomRockPaperScissors = RockPaperScissors(rawValue: Int.random(in: 1...3)) else { return isUserSelect }
        print(compareRockPaperScissors(between: randomRockPaperScissors, and: playerRockPaperScissors))
    case "0":
        isUserSelect = false
        print("게임 종료")
    default:
        print("잘못된 입력입니다. 다시 시도해주세요.")
    }
    return isUserSelect
}

func startGame() {
    var isUserSelect: Bool = true

    compareRockPaperScissors(between: randomRockPaperScissors, and: playerInput)
    repeat {
        isUserSelect = getUserInput()
    } while isUserSelect
}   
```
</details>


### 🔥 함수의 기능 분리
- `getUserInput()` 함수 내부에 사용자의 입력을 받고, 입력 받은 값을 조건과 비교하는 두 가지 기능이 있어 함수명과는 맞지 않는다고 생각되었습니다.
- 따라서 사용자 입력만을 받는 `getUserInput()`과 `checkUserInput()`으로 분리하여 구현하였습니다.

<details>
<summary>세부 사항</summary>

#### 수정 전
```swift
func getUserInput() -> Bool {
    var isGameInProgress: Bool = true
    
    print("가위(1), 바위(2), 보(3)! <종료 : 0> :", terminator: " ")
    guard let input = readLine() else { return isGameInProgress }

    switch input {
    case "1", "2", "3":
        guard let inputNumber = Int(input),
              let playerRockPaperScissors = RockPaperScissors(rawValue: inputNumber),
              let computerRockPaperScissors = RockPaperScissors(rawValue: Int.random(in: 1...3)) else {
            return isGameInProgress
        }
        print(compareRockPaperScissors(between: computerRockPaperScissors, and: playerRockPaperScissors))
    case "0":
        isGameInProgress = false
        print("게임 종료")
    default:
        print("잘못된 입력입니다. 다시 시도해주세요.")
    }
    return isGameInProgress
}
```

#### 수정 후
```swift
func getUserInput() -> String {
    print("가위(1), 바위(2), 보(3)! <종료 : 0> :", terminator: " ")
    guard let input = readLine() else { return "" }
    
    return input
}

func checkUserInput(_ userInput: String) -> Bool {
    var isGameInProgress: Bool = true
    
    switch userInput {
    case "1", "2", "3":
        guard let inputNumber = Int(userInput),
              let playerRockPaperScissors = RockPaperScissors(rawValue: inputNumber),
              let computerRockPaperScissors = RockPaperScissors(rawValue: Int.random(in: 1...3)) else {
            return isGameInProgress
        }
        isGameInProgress = !compareRockPaperScissors(between: computerRockPaperScissors, and: playerRockPaperScissors)
    case "0":
        isGameInProgress = false
        print("게임 종료")
    default:
        print("잘못된 입력입니다. 다시 시도해주세요.")
    }
    return isGameInProgress
}
```
</details>
    
### 

### 🔥 게임 종료
- 게임이 이기거나 졌을 경우에는 종료가 되어야 하는데 계속해서 실행되던 문제점이 발생하여 `compareRockPaperScissors()` 반환타입을 `Bool`로 변경해서 해결했습니다.
<details>
<summary>세부 사항</summary>

#### 수정 전
```swift
func compareRockPaperScissors(between computerRockPaperScissors: RockPaperScissors, and playerRockPaperScissors: RockPaperScissors) -> String {
    
    if computerRockPaperScissors == playerRockPaperScissors {
        return "비겼습니다!"
    }

    switch (computerRockPaperScissors, playerRockPaperScissors) {
    case (.paper, .scissors), (.scissors, .rock), (.rock, .paper):
        return "이겼습니다!"
    default:
        return "졌습니다!"
    }
}
```

#### 수정 후
```swift
func compareRockPaperScissors(between computerRockPaperScissors: RockPaperScissors, and playerRockPaperScissors: RockPaperScissors) -> Bool {
    var isGameOver: Bool = true

    switch (computerRockPaperScissors, playerRockPaperScissors) {
    case (.paper, .scissors), (.scissors, .rock), (.rock, .paper):
        print("이겼습니다!")
    case (.scissors, .paper), (.rock, .scissors), (.paper, .rock):
        print("졌습니다!")
    default:
        print("비겼습니다!")
        isGameOver = false
    }
    
    return isGameOver
}
```
</details>

### 🔥 가위바위보 승자가 먼저 공격
- 묵찌빠는 가위바위보 게임의 승자가 우선적으로 공격하기 때문에 `RockPaperScissorsGame`이 끝났을 때 결과를 리턴하도록 하였습니다.

<details>
<summary>세부 사항</summary>

#### 게임 결과를 리턴하는 코드
```swift
struct RockPaperScissorsGame {
    // ...

    mutating func startGame() -> GameResult {
        repeat {
            let userInput = getUserInput()
            checkUserInput(userInput)
            isGameInProgress = gameResult == nil ? true : false
        } while isGameInProgress
        
        guard let gameResult = gameResult else { return GameResult.gameOver }
        
        return gameResult
    }
}
```

#### 결과에 따라 차례를 결정하는 코드
```swift
struct MukJiPpaGame {
    // ...
    
    private mutating func checkRockPaperScissorsGameResult(_ gameResult: GameResult) {
        switch gameResult {
        case .victory:
            turn = "사용자"
        case .defeat:
            turn = "컴퓨터"
        case .gameOver:
            isGameInProgress = false
        }
    }

    // ...
}
```
</details>
    
### 🔥 묵찌빠 실행시 `nil`값이 나오는 문제
- `nil`이 나오는 문제를 해결하기 위해서 "게임 종료"라는 `case`를 하나 더 추가한 `GameResult`라는 열거형으로 변경했습니다.

<details>
<summary>세부 사항</summary>

#### 수정 전
```swift
enum Turn: String {
    case user = "사용자"
    case computer = "컴퓨터"
}
```

#### 수정 후
```swift
enum GameResult: String {
    case victory = "승리"
    case defeat = "패배"
    case gameOver = "게임 종료"
}
```
    
#### 사용 코드
```swift
private mutating func checkUserInput(_ userInput: String) {
        let gameOver: String = "0"
        
        switch userInput {
        case "1", "2", "3":
            // ...
        case gameOver:
            gameResult = .gameOver
            print("게임 종료")
        default:
            print("잘못된 입력입니다. 다시 시도해주세요.")
        }
    }
    
```
    
</details>
        
---

    
</br>
    
<a id="6."></a> 
## 6. 참고 링크
- [The Swift Language Guide - 제어문(Repeat-While)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/)
- [The Swift Language Guide - 삼항연산자](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Ternary-Conditional-Operator)
- [The Swift Docs](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/methods/), [개인 GitHub - mutating](https://github.com/jwonyLee/TIL/blob/master/iOS/Interview/Mutating.md)
 
--- 
    
</br>
    
<a id="7."></a>
## 7. 팀 회고
### 👏🏻 우리팀이 잘한 점
- `groundRull`을 초반에 작성하여 계획적으로 프로젝트를 진행했습니다.
- 시간 약속을 잘 지키고, 일정 조율이 원활했습니다.
- 서로 의견을 잘 수용하며 프로젝트를 진행했습니다.


### 👊🏻 우리팀이 개선할 점
- `README`를 조금 더 간결하게 작성하면 좋을 것 같습니다.
- 프로젝트 내용 꼼꼼하게 확인하고 적용하였으면 좋겠습니다.(누락되는 사항 없이)
- 프로젝트 진행 전 참고해야되는 문서를 함께 보았으면 좋았을 것 같습니다.

</br>
    
### 💜 서로에게 좋았던 점 피드백
#### Dear. Erick
    - 첫 시작과 끝맺음을 잘해주셨습니다.
    - 이론과 문법 부분에서 많은 가르침을 주셨습니다.(기본 문법, 삼항연산자, 접근 제어 등)
    - 코드 구현을 깔끔하게 잘 하시는 것 같습니다.
    - 상냥하고 차분하신 것 같습니다.
    - 배려를 많이 해주시고 의견 조율을 해주시려고 노력하셨습니다. (프로젝트 진행함에 있어서 트러블이 없었습니다.)
  
#### Dear. Karen
    - 저의 의견을 먼저 물어봐주며 많이 배려해주셨습니다.
    - 프로젝트에서 해야할 일을 먼저 제시해주시고 여러가지 팁들을 많이 알려주셨습니다.
    - 제가 놓치는 사소한 부분들도 잘 캐치해서 말해주셨습니다.
    - 프로젝트 이외에도 README나 스크럼 등 내용 정리를 잘해주셨습니다.
  
</br>
    
### :pray: 서로에게 아쉬웠던 점 피드백
#### Dear. Erick
    - 현재 본인의 코드 스타일과 지식에 자신감을 가지셨으면 좋겠습니다.


#### Dear. Karen
    - 사용해보고 싶은 코드나, 생각 난 코드를 머리로만 생각하는 것이 아닌 먼저 작성해보는 것도 좋을 것 같습니다.
    - 프로젝트의 전체적인 흐름을 많이 생각해보셔도 좋을 것 같습니다. 
