<h3 id="introduction-to-operating-systems">Introduction to Operating Systems</h3>
<p>개요 : 운영체제란 무엇인가, 운영체제의 목적, 운영체제 분류, 운영체제의 예, 운영체제의 구조</p>
 <br />
 <br />
<br />
<br />



<h3 id="1-운영체제란-무엇인가">1) 운영체제란 무엇인가</h3>
<p><strong>개념</strong>: 하드웨어 바로 위에 설치되어 다른 사용자, 다른 모든 하드웨어,소프트웨어와 연결하는 소프트웨어 계층</p>
<p><strong>목적</strong>: 자원을 효율적으로 관리하고, 사용자에게 형평성 있게 자원을 분배하기 위함
사용자가 컴퓨터 시스템을 편리하게 사용하도록 지원</p>
<pre><code>* HW자원: 프로세서, 기억장치, 입출력 장치 SW 자원: 프로세스, 파일, 메세지 등</code></pre><blockquote>
<p>자원관리(CPU 스케줄링, 메모리관리,  파일 시스템 관리, 디바이스관리), 제어(동작 제어, 사용자와 하드웨어 간의 상호작용 관리), 사용자 인터페이스 제공(직관적인 UX/UI 제공), 오류 처리와 보안 기능(시스템 오류 감지, 자원 접근 제어)</p>
</blockquote>
 <br />

<p><strong>커널</strong>: 운영체제의 핵심 부분으로 메모리에 상주하는 부분</p>
<p>일반적인 관점에선 커널을 포함한 각종 시스템 유틸리티를 운영체제라고 하지만, 개발자 관점에서의 운영체제는 곧 커널을 뜻함</p>
<br />
<br />
<br />
<br />


<h3 id="2-운영체제-분류">2) 운영체제 분류</h3>
<p>** 동시작업 가능 여부
**</p>
<ol>
<li><p>단일 작업: 한 번에 하나의 작업 처리     ex) MS-DOS</p>
</li>
<li><p>다중 작업: 동시에 두 개 작업 처리     ex) UNIX, Windows </p>
</li>
</ol>
<p>** 사용자의 수
**</p>
<ol>
<li><p>단일 사용자       ex) MS-DOS, Windows</p>
</li>
<li><p>다중 사용자: 동시접근 가능       ex) UNIX, NT server</p>
</li>
</ol>
<p>*<em>처리 방식
*</em></p>
<ol>
<li><p>일괄처리(batch processing): 작업을 모아서 한꺼번에 처리</p>
</li>
<li><p>시분할(time sharing): 여러 작업이 수행이 될 때 작은 시간 단위로 나누어 번갈아가면서 할당하는 것 (시간 데드라인이 없음)</p>
</li>
<li><p>실시간(realtime OS): 데드라인 있음, 정해진 시간 안에 처리가 보장 되어야 함   ex) 로봇제어, 반도체 장비, 원자로 제어</p>
</li>
</ol>
<br />


<blockquote>
<p><span style="color: red;">헷갈리기 쉬운 용어</span>
Multitasking, Multiprogramming, Time sharing, Multiprocess  =&gt; 여러 작업을 동시에 수행하는 것
vs.
Mutiprocessor  =&gt; 하나의 컴퓨터에 CPU(processor)가 여러 개 붙어 있음을 의미</p>
</blockquote>
<br />
<br />
<br />
<br />
<br />


<h3 id="3-운영체제-예">3) 운영체제 예</h3>
<p><strong>UNIX</strong>: 어셈블리 언어로 구현이 어려워서 C언어로 개발, 소스코드 공개, 높은 이식성(c언어로 구성되어 있어서 컴퓨터 간 이식성이 높음), 확장성, 커널 크기가 작음</p>
<p>ex) System V, FreeBSD, Linux</p>
<br />

<p><strong>MS Windows</strong>: 다중 작업용 GUI(Graphical User Interface)기반 운영체제, 풍부한 지원 소프트웨어</p>
<br />

<p><strong>macOS</strong>: 우수한 GUI와 성능 제공, 하드웨어와 소프트웨어의 통합 강조, iOS와의 통합성을 통해 애플 생태계 내에서 데이터 및 앱 공유</p>
<br />
<br />
<br />
<br />
<br />

<h3 id="4운영체제의-구조">4)운영체제의 구조</h3>
<p><strong>CPU 스케줄링</strong>: 일반적으로 짧은 시간 간격을 가지고 짧은 업무를 먼저 처리, 긴 업무를 뒤로 보내는 스케줄링을 따르지만 자원 특성을 최대한 활용하여 효율적인 스케줄링을 해야함
<br />
<strong>메모리 관리</strong>: 한정된 메모리를 어떻게 분배하는지에 대한 관리
<br />
<strong>파일 관리</strong>: 헤드가 움직이면서 처리하기 때문에 어디에 먼저 들를지 같은 요청을 처리(디스크 스케줄링)       ex) 엘리베이터, 택배
<br />
<strong>입출력 관리</strong>: 입출력장치와 CPU 간의 정보를 주고받기, '인터럽트'</p>
<br />