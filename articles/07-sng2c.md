# Perl Again in 2012

## 작성자 정보
* 작성일 : 2012-05-15
* 작성자 : 김현승 (sng2nara@hanmail.net)

 
## Abstraction
오래전 우리나라에서는 잊혀지고만 perl을 재조명해봅니다.
 
## 내용
![Perl Logo](http://quicksilver1183.com/wp-content/uploads/2012/02/perl_logo.jpg)


저는 펄을 처음 만난게 98년 대학 1학년 여름방학때였습니다. 방명록하나 만들어보려고 이게 펄인지 뭔지도 모른채 앞뒤만 맞추던 꼬꼬마때로군요. 벌써 14년이...ㅠㅠ

Perl은 언어학자인 Larry Wall이 1987년에 언어학,컴퓨터사이언스,예술성,상식을 버무려서 만들어낸 언어입니다. 제가 초딩때군요.
![Larry](http://upload.wikimedia.org/wikipedia/commons/thumb/b/b3/Larry_Wall_YAPC_2007.jpg/225px-Larry_Wall_YAPC_2007.jpg)

C와 쉘스크립트만 있는 1차원적인 unix세계에 펄이 끼어들어서 신세계를 보여주었습니다. 아직도 linux에서는 펄에 의존성이 높아 배포판에 포함되어 있습니다.

Larry Wall 이 ['펄의 과거,현재 그리고 미래'](http://www.joinc.co.kr/modules/moniwiki/wiki.php/Site/JPerl/PerlPresentFuture) 에서 아래와 같이 다른 프로그래밍 언어들에 대해 기본적인 설계철학에 대해서 이야기했습니다.

## 프로그래밍 언어들의 내재된 의도

* "밑 바닥부터 모조리 갈아엎고 시작해야 한다." - 대부분의 학문적인 언어
* "영어 표현" - 그것은 Cobol. 카고컬트(남태평양의 원주민들이 미군이 비행기로 화물을 실어 와서 착륙하던걸 보고 다시 비행기가 착륙하여 자기들을 구원해주고 도와주기를 바라는 신앙- 다시는 일어나지 않을 어이없는것을 바라는 어리석음을 뜻함) 영어. (웃음)
* "문자열 처리는 중요한 문제가 아니다" - Fortran.
* "간단한 언어는 간단한 해결책을 만든다." - C.
* "빨라지길 바란다면 C로 만들것이다." - 원본 awk 페이지로 부터의 거의 직접적인 인용
* "나는 어떻게 해야할지 생각을 했다. 따라서 그것은 올바른것이 틀림없다." - 그것은 명백하게 PHP. (웃음과 박수)
* "무엇이라도 NAND게이트로 만들 수 있다." - 전자공학자에 의해 만들어진 아무 언어들. (웃음)
* "이것은 고차원 언어이다. 누가 bit를 신경쓰느냐?" - 4세대 언어의 전 영역이 이 문제에 봉착함
* "사용자는 우아함에 신경쓴다." - 유럽쪽에서 만들어진 많은 언어들이 여기에 봉착함, Eiffel.
* "언어명세(specification)가 충분히 좋다." - Ada.
* "추상화는 사용성과 같다." - Scheme. 그와 비슷한 언어들.
* "일반 핵심(common kernel)은 가능한한 작아야 한다." - Forth.
* "컴퓨터가 알아먹기 쉽게 만들자" - Lisp.(웃음)
* "대부분 프로그램이 하향식으로 설계되어진다." - Pascal.(웃음)
* "모든것은 벡터다" - APL.
* "모든것은 객체다" - Smalltalk 와 그 파생언어들. (속삭이며:) Ruby. (웃음)
* "모든것은 가설이다." - Prolog. (웃음)
* "모든것은 함수이다." - Haskell. (웃음)
* "프로그래머에게는 주어진 자유의지가 있어서는 안된다." - 명백하게, Python. (웃음)

## 펄의 내재된 철학 

위와 같이 언어마다 기본이 되는 설계 철학이 있다고 이야기하고는 펄에 내재된 철학에 대해서 설명을 합니다.

* 언어학 : 배우기 쉬운 것보다 표현력이 좋아야 한다. 사람에 따라 표현력의 차이는 있지만, 말을 못하는 것은 아니다.
* 인류학 : 세계에서 가장 큰 시시한 소프트웨어들의 저장소인 [CPAN](http://www.cpan.org) 으로 서로서로 공유하고, 지식을 얻을수 있게 하였다.

펄은 상황(Context)에 따라 다르게 작동하는 특성, 수많은 기호(연산자), 많은 키워드들로 인해 처음 익히기는 어렵지만, 익히고 나면 하나의 문제에 대해 다양하게 표현할 수 있게 됩니다.

코드골프에서 펄이 항상 1등을 하는 이유가 뭘까요?
그건 바로 자주 마주치는 복잡한 문제들을 몇개의 단어로 추상화하여, 어휘력(키워드)를 늘린 것이 가장 큰 이유일 것입니다. 그래서 사용자라이브러리를 쓰지 않은 소스코드가 유난히 짧을 수 있습니다.

쉘에서 쉘스크립트대신 1줄로 뭔가를 처리하고 싶을 때, 한번 쓰고 버릴 코드를 위해 변수명을 일일이 지정하는 것이 의미없을 때, 구조화를 통해 무결점의 프로덕트를 만들어야 할 때.
모두 펄을 통해서 가능합니다.

## 펄의 악명

펄의 악명은 4버전때와 5버전초기에 나온 것입니다.

* 펄은 가독성이 낮다.
* 펄은 느리다.
* 펄은 확장이 힘들다.
* 펄은 CGI용 언어이다.
* 펄은 죽었다.

개중에는 경쟁언어의 추종자들이 퍼뜨린 낭설도 있긴 하지만, 적어도 국내에서는 죽었다고 보는 시각이 많습니다.
주류 언어로 자리잡지 못한데에는 운명같은 그런 이유가 있기 때문인데요.

1. 한물간 언어 : Dynamic 웹이 고개를 들면서 CGI의 빈틈을 PHP가 채웠다.
2. 상용화 실패 : 펄은 바이트코드 결과물이 없다.(파이썬의 pyc같은)
3. 신규 유입 실패 : 비주얼한 결과물이 쉽게 나오지 않는다.

왜 파이썬과 루비에는 열광하는데, 펄에는 그러지 않을까요?

1. 파이썬은 스크립트언어이지만 상용화 될수 있다는 점이 매력적이고, 실제로 단일 exe파일로도 잘 만들어집니다. Tkinter라는 GUI라이브러리도 기본으로 탑재하고 있습니다.
2. 루비는 깨알같은 객체지향 구현을 보여주면서, 숙달된 CSS전문가의 도움으로 Ruby on rails의 기본 결과물이 아주 이뻤습니다. ROR == Ruby 일 정도로 매력적이었습니다.
3. 펄은 그런거 없었습니다.


## 모던 펄(Modern Perl) 

지금 펄의 버전이 궁금하신가요?

우리회사의 대부분의 서버에는 5.6버전대와 5.8버전대가 깔려있고, 새로 설치되는 서버에는 5.10이 설치되고 있습니다. 5.1.0이 아니예요. 10번째 버전입니다.
그리고 릴리즈된 최근 버전은 5.14입니다. emacs의 버전이 무려 23.4인것에 비하면 초라하지만, 14번째 메이저 업데이트를 하면서 점차 문법자체를 사용자가 바꿀 수 있는
'어휘력','확장성'에 무게를 두고 발전해 나가고 있습니다.

![Modern Perl](http://onyxneon.com/books/modern_perl/mp_cover_med.png)

최근 몇년간 모던펄로 접어들면서, 펄계는 엘레강스하면서 신속하고 간결한 구현에 초점을 맞추고 있습니다.

튼튼한 기존세력([펄을 이끄는 인물들](http://aero.springnote.com/pages/159748), 이중 오드리 탕이 제 [모듈](https://metacpan.org/module/Template::Reverse)에 관심을 보였다능..)들과 함께 여러 새로운 피들(대표적으로 [Miyagawa](https://metacpan.org/author/MIYAGAWA) 엄청난 모듈생산력!!)이 나타나서 활력을 불어넣고 있으며
트렌드에 맞춰 실용적인 모듈들과 아티클들이 열정적으로 생산되고 있습니다.

이만 하면, 트렌드를 선도한다고 봐도 무리가 없을텐데요.

### CPAN (Comprehensive Perl Archive Network)

무려 1995년에 만들어진 최초의 Social 코딩 서비스입니다.
간단한 쉘명령어(cpan 또는 cpanm)로 모듈을 검색해서 자동으로 설치할 수 있고, 의존성도 자동으로 해결하며, [테스팅프레임웍](http://matrix.cpantesters.org/?dist=WWW-Mechanize-1.72)이 갖춰져 있어서, 기부된 수많은 시스템에서의 테스트결과를 확인할 수 있습니다.

최근에는 세련된 디자인의 https://metacpan.org 을 즐겨씁니다.

### OOP

펄은 OOP안되지 않나? 쉘스크립트 같은거 아닌가?

땡입니다.

파이썬의 OOP모델을 기반으로 minimum으로 구현한 펄의 OOP도 [Moose](https://metacpan.org/module/Moose)라는 고급 OOP라이브러리를 통해 한층 성숙하고 있습니다.
[새로운 OOP로 개과천선하기](http://bit.ly/IVIHVS)

### 웹프레임웍

요즘은 Scalable한 것과 FastCGI+nginx의 조합으로 non-block IO로 군더더기 없이 처리하는 것이 트렌트이지요?
펄의 웹프레임웍도 이게 됩니다.

펄에는 파이썬의 WSGI를 펄식으로 옮긴 [PSGI](https://metacpan.org/module/PSGI)가 있습니다.

MVC기반의 표준 웹프레임웍인 [Catalyst](https://metacpan.org/module/Catalyst)도 있습니다. PSGI와 호환되구요.
그 외 경량 웹프레임웍인 [Mojolicious](https://metacpan.org/module/Mojolicious)와 [Dancer](https://metacpan.org/module/Dancer)도 있습니다. 
이 둘도 모두 PSGI와 호환됩니다.

그리고 모두 FastCGI로 돌릴수 있구요.

민폐CGI로만 펄을 떠올리던 시절은 이미 갔습니다.

### SNS

[Facebook](https://metacpan.org/module/Facebook), [Net::Twitter](https://metacpan.org/module/Net::Twitter), [WWW::LinkedIn](https://metacpan.org/module/WWW::LinkedIn) 등과 같이
API가 공개되는 족족 구현물이 CPAN에 등록되고, 남아도는 열정으로 플러그인까지도 만들어 냅니다.
특히 트위터 모듈의 경우에는 Python의 그것보다 훨씬 영리하게 페이징과 예외처리,API호출빈도 관리등을 할 수 있게 해줍니다.

저도 얼마전 공개된 마이피플봇인 똑똑박사처럼 똑똑한 아이를 만들어보려고, Net::MyPeople 을 digit(daum 사내 repository)에 등록해 놓기도 했습니다.

### libev

libev는 node.js의 이벤트 루프의 핵심이 되는 라이브러리입니다. 

사실 이것은 펄해커인 마크 레만씨가 펄에 이벤트 드리븐 프로그래밍을 도입하려고 만든 [EV](https://metacpan.org/module/EV)라이브러리의 일부였습니다.

## Perl6 가 있던데?

![Perl6 Logo](http://www.perl6.org/camelia-logo.png)

펄6는 펄7으로 가기 위한 실험체로 알려져 있습니다. 펄5와 공존하면서 가는 것이죠. 얼핏 보면 perl5에서 갈라진 루비와 비슷한 길을 가는 것 같지만, 실상은 전혀 다릅니다.

그동안 펄5를 사용해왔던 각계각층의 기술자들이 자신들의 노하우를 제안하고 Core에 녹이면서 엄청난 플랫폼이 되어가고 있습니다.

![Parrot](http://www.parrot.org/sites/www.parrot.org/files/parrotify_logo.png)

결국 프로젝트 초기에 VM(인터프리터)를 분리하면서 [Parrot](http://www.parrot.org/)이라는 레지스터기반 VM프로젝트가 파생되었고, 
무서운 속도로 [릴리즈](http://www.parrot.org/category/news/news)를 해가고 있습니다. 

저는 잘 이해가 안되지만 레지스터기반이라 거의 [모든 인터프리팅언어](http://trac.parrot.org/parrot/wiki/Languages)들을 VM위에 올릴수 있다고 합니다. 
심지어는 닷넷과 자바도 컴파일하여 돌릴수 있고, Parrot바이트코드를 닷넷이나 자바바이트코드로 번역해 그 위에서 돌리는것도 어렵지 않다고 합니다.

펄6는 매일 같이 스펙이 바뀌는 통에, 회사일을 해야하는 저로써는 엄두가 안나서 접근을 안하고 있습니다.

## 내 주위에는 펄하는 사람이 없는데 누구랑 기쁨을 나눠야 하나요?

있습니다. 서울에도 많구요.(그렇게 많지는 않습니다만)

고전적이게도 IRC에 상주를 하는 사람들이 있고, 이 사람들이 우리나라 펄커뮤니티 활동의 주류입니다.
저도 한때는 펄마니아의 시삽으로써 전성기를 누렸으나, 회사일에 더 재미를 느끼는 바람에, 펄마니아마저 좌초되고 말았답니다. 흐규흐규

chat.freenode.net:6667 서버에 #perl-kr 에 가시면 20명 남짓한 상주자들을 만날 수 있습니다.
이들은 펄몽거스( http://seoul.pm.org , http://www.perl.kr/ )의 서울지부(?)원들이고, 펄로만 일을 하는 사일렉스라는 회사를 차려서, 국내 최초의 펄빠만의 회사를 만들었습니다.
건대역근처에 있으니 관심있으시면 동호회 활동삼아 견학도 가능(?).

http://advent.perl.kr/2011/ 이 링크로 가시면 이 분들의 열정과 함께, 펄이 썩어가는 언어가 아니었구나 하는 것도 함께 느끼실 수 있습니다.

그리고 네이버에 있는(슬픈일이지만) 펄초보카페 등에서도 여러 사람들을 만날 수 있습니다.

## 이 글을 읽고 나니 펄에 대해서 더 알고 싶습니다. 어떻게 해야하나요?

최근에 번역판이 하나 펄몽거스분들에 의해 태어났는데요. '거침없이 배우는 펄'(저랑은 아무런 이해관계가 없습니다.)을 보시길 추천합니다.
한줄 한줄 따라가다 보면, 어라? 이거 다르네? 하며 신선한 충격을 받으실 거예요. 펄만의 매력이라 믿고 있습니다.

그리고 저(김현승 sng2nara@hanmail.net)에게 문의주시면 펄학습에 대한 정확하고 빠른 방법을 알려드릴테니 연락주시길 바라겠습니다.
