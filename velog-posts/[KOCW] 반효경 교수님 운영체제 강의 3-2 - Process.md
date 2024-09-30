<p>개요: Thread, Single and Multithreaded Processes, Benefits of Threads, implementation of threads</p>
<p> <br /><br /><br /><br /></p>
<h3 id="1-thread-lightweight-process">1) Thread (=Lightweight Process)</h3>
<p>: 스레드는 CPU 수행의 기본 단위 또는 프로세스 안의 제어권의 흐름</p>
<p>스레드가 수행되는 환경을 Task라고 부르며, 전통적 프로세스는 하나의 스레드를 가진 Task(싱글 스레드)이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/a02255c7-f805-4e47-929f-508c40bda11b/image.png" />
<a href="https://rebro.kr/174">링크텍스트</a></p>
<p>같은 일을 하는 프로세스를 여러 개 띄우고 싶다면 굳이 메모리 공간을 각각 띄워놓기 보다
프로세스마다 다른 부분의 코드만(일부만) 실행할 수 있게 하면 된다. 
(= 멀티 스레드 : 하나의 프로세스에 여러 개 스레드)</p>
<blockquote>
<p>Multithead의 예시: web 브라우저(화면 출력 스레드, 데이터 읽어오는 스레드)
word porcessor(화면 출력 스레드, 키보드 입력 스레드, 철자/문법오류 확인 스레드)</p>
</blockquote>
<p> <br /><br /><br /></p>
<h3 id="2-thread-구성-스레드가-독립적으로-가져야-하는-것">2) Thread 구성 (스레드가 독립적으로 가져야 하는 것)</h3>
<p>Program Counter 
Register set
Stack</p>
<p><br /><br /></p>
<h3 id="2-1-thread가-동료-thread와-공유하는-부분task">2-1) Thread가 동료 Thread와 공유하는 부분(=task)</h3>
<p>Code section
data section
OS resources</p>
<p> <br /><br /><br /><br /></p>
<h3 id="3-thread의-장점">3) Thread의 장점</h3>
<ul>
<li>응답성(프로세스 생성에 비해 스레드 생성 시간이 더 빠르기 때문)</li>
<li>자원 공유(스레드 간 프로세스 자원을 공유할 수 있다), 통신 비용이 적음</li>
<li>오버헤드가 적다</li>
<li>작업을 병렬처리 가능</li>
</ul>
<p>  <br /><br /><br /><br /></p>
<h3 id="4-커널-레벨-스레드-vs-유저-레벨-스레드">4) 커널 레벨 스레드 vs. 유저 레벨 스레드</h3>
<ul>
<li><p><strong>Kernel-Level Thread</strong>: 커널이 스레드가 여러 개인 것을 알고 있음</p>
</li>
<li><p><strong>User-Level Thread</strong>: 사용자 레벨의 라이브러리를 통해 구현되며 커널이 스레드를 인식하지 못함</p>
</li>
</ul>