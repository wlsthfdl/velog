<p>개요: 프로세스의 개념, 프로세스의 상태, PCB, 문맥교환, 프로세스 스케줄링 큐, 스케줄러, Ready Queue/Device Queue</p>
<br />

<h3 id="1-프로세스의-개념">1) 프로세스의 개념</h3>
<p>실행 중인 프로그램. 디스크에 실행파일 상태로 존재하던 프로그램이 메모리에 올라가서 실행되기 시작하면 비로소 생명력을 갖는 프로세스가 된다.
<br />
<br />
<br /></p>
<h3 id="2-프로세스의-문맥context">2) 프로세스의 문맥(Context)</h3>
<p>여러 프로세스가 수행되는 환경에선 CPU를 빼앗기고 획득함을 반복하게 되는데, 이전 CPU보유 시기에 어느 부분까지 수행했는지 정확한 상태를 재현할 필요가 있다. 
이 때 필요한 정보가 '프로세스의 문맥'</p>
<ul>
<li>CPU 수행 상태를 나타내는 하드웨어 문맥 (현재 시점 기준)</li>
<li><em>Register, Program Counter(PC)*</em></li>
<li>프로세스 주소공간</li>
<li><em>Code, Data, Stack*</em></li>
<li>프로세스 관련 자료구조</li>
<li><em>PCB(procss control block)*</em></li>
<li><em>Kernel Stack *</em>: 시스템 콜을 하면 PC가 커널의 code를 가리키며 수행되는데, 호출 정보를 커널 스택에 프로세스 별로 두어서 저장</li>
</ul>
<br />
<br />
<br />
<br />

<h3 id="3-프로세스의-상태">3) 프로세스의 상태</h3>
<ul>
<li>실행(Running) : CPU를 잡고 수행 중인 상태</li>
<li>준비(Ready) : 물리 메모리에 올라가 있고, 모든 준비를 끝마친 CPU만 잡으면 되는 상태</li>
<li>봉쇄(Blocked, Wait, Sleep): CPU를 할당 받더라도 당장 instruction을 수행할 수 없는 상태</li>
</ul>
<p>추가 + </p>
<ul>
<li>시작(New): 프로세스를 생성 중인 상태</li>
<li>완료(Terminated): 수행이 끝난 상태</li>
</ul>
<p><br /><br /><br /></p>
<h3 id="3-1-프로세스-상태도">3-1) 프로세스 상태도</h3>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/61143227-e9b3-4a88-8d41-7a448d8ec376/image.png" /></p>
<p><br /><br /><br /></p>
<h3 id="3-2-상태-전환-예시">3-2) 상태 전환 예시</h3>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/5f6571cb-d2cd-4d74-9529-facac7dfefb5/image.png" /></p>
<p><br /><br /><br /><br /></p>
<h3 id="4-pcb-process-control-block">4) PCB (Process Control Block)</h3>
<p>: 운영체제가 각 프로세스를 관리하기 위해 프로세스 당 유지하는 정보</p>
<ul>
<li>OS가 관리상 사용하는 정보: process state, process ID, CPU 스케줄링 정보, 프로세스 우선순위 등</li>
<li>CPU 수행 관련 하드웨어 값: program counter, register</li>
<li>메모리 관련: code, stack, data 위치 정보</li>
<li>파일 관련: Open file descriptors</li>
</ul>
<p><br /><br /><br /><br /></p>
<h3 id="5-문맥교환context-switch">5) 문맥교환(Context Switch)</h3>
<p>: CPU를 A프로세스에서 B프로세스로 넘겨주는 과정</p>
<p>그 과정에서 OS는 다음을 수행</p>
<blockquote>
<p>CPU를 내어주는 프로세스 상태를 그 프로세스 PCB에 저장
CPU를 새롭게 얻는 프로세스의 상태를 PCB에서 읽어옴</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/e867ada7-851d-4dd6-9b8c-374e693fa695/image.png" /></p>
<p>※ System call이나 interrupt는 반드시 문맥교환이라고 할 수 없음</p>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/6c64c7b2-5383-461b-9790-318332af1d13/image.png" /></p>
<p>위의 예시의 경우에도 context의 일부를 PCB에 저장해야 하지만, context switching을 하는 아래의 예시 경우 그 부담이 훨씬 크다.</p>
<blockquote>
<p>참고: 
프로세스에서 문맥교환이 일어났을 경우, PCB 구조상 공유하는 데이터가 없으므로 캐시가 쌓아온 데이터들이 무너지고 새로운 캐시 정보를 불러와야 하기 때문에 부담이 간다.
반면, 스레드 문맥교환은 스레드가 바뀌어도 공유하는 데이터가 있기 때문에 프로세스 문맥교환에 비해 빠르다.
<a href="https://80000coding.oopy.io/ef52431e-cf52-497b-824f-bcb365144c7a">링크텍스트</a></p>
</blockquote>
<br />
<br />
<br />
<br />

<h3 id="6-프로세스를-스케줄링하기-위한-큐">6) 프로세스를 스케줄링하기 위한 큐</h3>
<ul>
<li>Job Queue: 현재 시스템 내에 있는 모든 프로세스 집합</li>
<li>Ready Queue: CPU가 잡히길 기다리는 큐. 메모리에 있음</li>
<li>Device Queue: I/O Device의 처리를 기다리는 큐 (blocked, asleep상태). Device Controller에 있음</li>
</ul>
 <br />
<br />
<br />
<br />


<h3 id="7-스케줄러">7) 스케줄러</h3>
<blockquote>
<ul>
<li><strong>Long-term Schedular (Job Schedular)</strong>: 어떤 프로세스를 Ready Queue에(메모리 load) 보낼지 결정. 하지만 현대의 시분할 시스템에서의 OS는 일반적으로 장기 스케줄러를 두지 않음 =&gt; Medium Schedular로 올림</li>
</ul>
</blockquote>
<ul>
<li><strong>Short-term Schedular (CPU Schedular)</strong>: 현재 메모리에 올라와있는 프로세스 중 어떤 프로세스를 CPU 점유권을 가질지 결정하는 스케줄러</li>
<li><strong>Medium-term Schedular (Swapper)</strong>: 만약 asleep 상태에서 ready로 넘어가지 못하거나 ready에서 running 상태로 넘어가지 못하는 상황이 발생하면, 실행은 되지 않고 메모리만 잡아먹고 있는 비효율적인 상황이 된다.
이럴 경우를 위해 메모리에 load 되어 있는 비효율 프로세스를 다시 하드디스크로 쫓아내는 것이 Swap-out이고, 다시 메모리로 올리는 것이 Swap-in이다. 이 과정을 스케줄링 하는 것이 바로 Medium-term Schedular이다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/5a805afc-39b8-42b9-b638-925129faf07f/image.png" />
중기 스케줄러로 인해 한 가지 프로세스의 상태가 더 생긴다</p>
<p><strong>Suspended</strong> 상태: 외부적으로 프로세스 수행이 일시정지 된 상태</p>
<p>ex) 사용자가 프로그램 일시정지시킨 경우, 시스템이 여러 이유로 중단시킨 경우 ==&gt; 외부에서 재개해 주어야 함</p>
<br />
<br />
<br />