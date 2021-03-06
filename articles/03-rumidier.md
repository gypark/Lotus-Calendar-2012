셋째날 : 인터넷 사전을 쉘에서 사용하고 싶다
===========================================

글쓴이
======

@rumidier, 꽃집아들, 해병대900대기수, 한영어린이

## 개요

 뛰어난 개발자를 꿈꾸며 원서를 읽어 보지만 모르는 단어가 너무 많습니다.
시도 때도 없이 단어 검색을 하느라 문서 보랴 단어 검색 하랴 코딩 해보랴
키보드 칠 시간에 마우스질 하느라 더 바쁩니다. 더불어 검색중 흥미 있는
기사거리를 보면 헬게이트가 열리게 되죠.....
그래서 마우스를 건들지 않기 위해 초보 펄게이가 간단한 사전을 만들어 보았습니다.
초보 펄게이는 만들수 있는게 한정 되있기 때문에 거대한 사전을 만들수 없으니
N이놈 에서 읽어 오는 방식을 택하였습니다. 초보 펄게이와 함께 열반에 들어 봅시다.

## 개발 환경 및 전제조건
 1. 리눅스(우분투)에서 개발, 실행 하였습니다.
 1. HTML트리는 firebug를 활용하였습니다.
 1. 많은 테스트 데이터가 없어 불안정 하므로 수정이 필요 합니다.
 1. 원하는 내역이 나오지 않는다면 수정 부탁드립니다.

## 사용된 모듈
- utf8
- LWP::UserAgent
- HTML::TreeBuilder
- HTML::Element

## 웹페이지 읽어 오기

인자(단어)를 LWP::UserAgent URL인자 전달에 알맞게 집어 넣습니다($search_n)
원활하게 읽어 들이게 된다면 $lists에 웹페이지 내용이 읽어 들여 집니다.

<pre class="brush: perl">
    my $ua = LWP::UserAgent->new;
    $ua->timeout(10);
    $ua->env_proxy;
    
    my $search_n = $ARGV[0];
    my $response = $ua->get("http://endic.naver.com/popManager.nhn?m=search&searchOption=&query=$search_n");
    my $lists;
    $response->is_success ? $lists = $response->decoded_content : die $response->status_line;
</pre>

## 상태 확인하기

HTML::TreeBuilder를 사용하여 검색 단어가 동사, 명사, 형용사등의 내용이
있는지 확인 하여 정적인 검색을 원활하게 할수 있도록 범위를 한정 합니다.

<pre class="brush: perl">
    my $tree = HTML::TreeBuilder->new();
    $tree->parse($lists);
    $tree->eof;

    my $links;
    my $dic_select;
    $dic_select = $tree->look_down('class', 'list_select');

    if (!$dic_select) {
        my @body_selects = $tree->look_down('class', qr/word_num word_num2 .*?$/);

        for my $body_select (@body_selects) {
            print_body($body_select);
        }
    }
    else {
        my $select_value = $dic_select->look_down('class', "underlink N=a:pos.tab");
        $select_value->as_text ? print_word() : print_idiom();
    }
</pre>

## print_body (본문)

*in*, *for*, *our* 등을 검색 했을시는 class가, list_select인 항목이 없으므로 
본문의 내용만 출력 합니다.

<pre class="brush: perl">
    sub print_body {
        my $body_select = shift;
    
        my $body_check = $body_select->look_down('alt', '본문');
    
        if ($body_check) {
            say "[본문]";
            my @ere = $body_select->look_down('class', 'fnt_e30');
            say $_->as_text for @ere;
        }
    }
</pre>

## 출력 화면

<pre class="brush: bash">
    $./view.pl our
    [본문]
    저희들의 
    우리2 
    저희 
    우리 집 
    우리 편 
</pre>

## print_idiom

*naver* *daum* 등을 검색 했을시 list_select 값이 존재 하지만 명사, 형용사등에 대해서는
존재 하지 않습니다. 하지만 필요한 검색 내역은 있으므로 그 부분을 출력 합니다.

<pre class="brush: perl">
    sub print_idiom {
       say "[뜻]";
       my $mean = $tree->look_down('class', "first align_px mean_on");
       say $mean->as_text;
    }
</pre>

## 출력 화면

<pre class="brush: bash">
    $ ./view.pl naver
    [뜻]
    (인터넷) 네이버, NHN(주)에서 제공하는 인터넷 포털사이트 
</pre>

## print_word
 
 list_select 포함되어 있는 단어들의 뜻과 형을 확인 합니다.

<pre class="brush: perl">
    sub print_word {
        my @words   = $tree->look_down('class', qr/box_wrap1 .*?/);
        $dic_select = $tree->look_down('class', 'list_select');

        for my $word (@words) {
            my $dic_tit     = $word->look_down('class', 'dic_tit6');
            my @align_lines = $word->look_down('class', qr/ mean_on/);
            say $dic_tit->as_text;

            for my $align_line (@align_lines) {
                say $align_line->as_text;
            }
        }
    }
</pre>

## 출력 화면

<pre class="brush: bash">
    $ ./view.pl happy
    형용사(hap・pier , hap・pi・est), (참고: mean n.)
    1. FEELING/GIVING PLEASURE |  ~ (to do sth) | ~ (for sb) | ~ (that…) (사람이) 행복한[기쁜]  
    1. FEELING/GIVING PLEASURE |   (일이) 행복한  
    1. AT CELEBRATION |   (Happy Birthday나 Happy New Year 같은 축하 인사에서 쓰임) 
    1. SATISFIED |  ~ (with/about sb/sth) 마음에 드는, 만족스러운; 마음이 놓이는  
    1. WILLING |  ~ to do sth (격식) 기꺼이 ~하는; ~하게 되어 기쁜  
    1. LUCKY |   운 좋은, 다행스러운  
    1. SUITABLE |   (격식) 말・생각・행동이 적절한  
</pre>

## PATH 추가

.bashrc에 경로를 추가후 언제 어디서든 view.pl [단어]를 사용하여 검색 하면 됩니다.

<pre class="brush: bash">
    export PATH=$PATH:"/home/meadow/rumidier"
    $ source .bashrc
</pre>

## 맺음말

초보 펄게이 이기 때문에 멋드러진 코드는 아닙니다만 저같이 배우면서 사용할수도 있는
좋겠다 생각 해서 이렇게 좋은날 올려 보게 되었습니다.

머리속에는 MySQL과 Dancer등을 사용해서 더욱 멋드러지게 나만의 사전을 만들고 싶었지만
많은 시간이 필요 할듯해서 여기 까지의 내용만 올리게 되어서 아쉽습니다.
아쉬운 부분은 더 배워 가면서 차근히 진행해 볼 생각 입니다.

나무아미타불 관세음보살

