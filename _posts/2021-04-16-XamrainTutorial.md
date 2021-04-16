---
title: "Xamarin 튜토리얼 #1"
date: 2021-4-16 21:23:28 -0400
categories: Xamarin
---

# Xamarin 수업

## Xamarin,IOS 및 Xamarin.Andriod

Xamarion 계층과 Xamarin.Forms 계층

- 자마린 계층
    - 안드로이드와 IOS 운영 체제 서비스에 대한 C#엑세스를 제공
    - e.g.) C#을 사용해서 java.lang.string 개체 또는 안드로이드 텍스트 입력에 엑세스 할 수 있다.
    - .NET 도 제공한다.
        - List<T>, HttpClient, ... 같은 항목.
    - **이 계층만을 이용해서 앱을 만드는 경우에는 UI 이벤트 같은 인터페이스 처리를 운영체제에 맞게 개별적으로 만들어야한다.**
- Xamarin.Forms 계층
    - UI 및 UI 동작을 한번만 정의해서 모든 운영체제에 공통적으로 정의하기 위해서 사용한다.

## Xamarin.Forms 에서 제공하는 것은?

- 페이지를 디자인하기 위한 정교한 레이아웃 엔진
- 서랍과 같은 다양한 탐색 형식을 만들기 위한 여러 페이지 형식
- 세련되고 유지 관리하기 쉬운 개발 패턴을 위한 XAML 및 데이터 바인딩 지원

## Xamarin.Essentials

UI와 관련 없는 모바일 앱의 다양한 일반적인 요구 사항을 처리

GPS, 가속도계, 배터리 및 네트워크 상태에 엑세스 가능.

## IOS와 Android 프로젝트

진입점

- IOS : `FinishedLaunching(...)`
- Android : MainActivity.cs 파일의 `OnCreate(...)`

# Application 클래스

- 앱의 수명 주기 이벤트를 처리하는 메소드를 가지고 있음.
    - `OnSleep, OnStart, OnResume`
    - 모달 스택의 변경에 응답하는 이벤트 **( ?????? )**
    - Properties 라는 속성 ⇒ 추가된 데이터를 자동으로 유지하는 `propertyBag`

# 페이지

Page는 Xamarin.Forms에서 UI 계층 구조의 root 로 사용된다.

일반적인 페이지 형식은 `ContentPage` 이고 다른 다양한 기능의 페이지를 지원한다.

- `NavigationPage`:
    - 친숙한 탐색 모음을 화면 위쪽에 추가하고 탐색 스택을 관리.
    - 이 스택을 통해 사용자가 이전 화면으로 뒤로 이동할 수 있음.
- `TabbedPage`
    - 탭 탐색에 사용되는 루트 페이지.
- `MasterDetailPage`
    - 서랍 형식 탐색 및 분할 보기를 호스팅.
    - 두 가지 주요 속성인 `Master` 및 `Detail`이 있으며, 각각에 `ContentPage`가 할당됩니다.

다른 다양한 페이지 기능은 추후에 살펴보자!

### Ex.) 페이지에 직접 버튼 추가하기

```csharp
public partial class MainPage : ContentPage
    {
        public MainPage()
        {
            InitializeComponent();

            var button = new Button()
            {
                Text = "Click Me"
            };
            button.Clicked += OnClick;

            RootLayout.Children.Add(button);
        }

        void OnClick(object sender, EventArgs e) { /*do something*/ }
    }
```

## 레이아웃

![Xamarin%20%E1%84%89%E1%85%AE%E1%84%8B%E1%85%A5%E1%86%B8%20675d17edf2074eccbe070835853cc7e2/Untitled.png](Xamarin%20%E1%84%89%E1%85%AE%E1%84%8B%E1%85%A5%E1%86%B8%20675d17edf2074eccbe070835853cc7e2/Untitled.png)

- `StackLayout`
    - 방향 속성에 따라 위쪽에서 아래쪽 또는 왼쪽에서 오른쪽 스택에 컨트롤을 배치합니다.
- `AbsoluteLayout`
    - 컨트롤에 대한 정확한 좌표를 설정할 수 있습니다.
- `RelativeLayout`
    - 여러 컨트롤의 크기와 모양 간의 관계를 정의할 수 있습니다.
    - 예를 들어 `button1`은 `entry1` 크기의 50%이고 5포인트 아래여야 합니다.
- `Grid`
    - 설정한 열과 행의 위치에 따라 해당 컨트롤을 배치합니다.
    - 열과 행의 크기 및 범위를 정의할 수 있으므로 그리드 레이아웃이 반드시 "바둑판 모양"이 될 필요가 없습니다.
- `ScrollView`
    - 하나의 자식만 직접 보유하므로 기술적으로 레이아웃으로 간주되지 않지만 화면 레이아웃에 매우 중요합니다.
    - 기본적으로 다른 모든 레이아웃은 실제로 필요한 경우 한 화면에 맞게 해당 콘텐츠를 압축하려고 시도합니다.
    - 그러나 이러한 다른 레이아웃을 ScrollView 내에 배치하면 화면을 스크롤할 수 있으며 콘텐츠를 압축할 필요가 없습니다.