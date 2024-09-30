<p>개요: 컴퓨터 시스템 구조, Mode bit, Timer Interrupt, I/O Device controller, DMA Controller, I/O의 수행, 시스템 콜, 인터럽트,  Synchronous/Asynchronous 입출력, Memory Mapped I/O, 저장장치 계층구조, 캐싱, 프로그램 실행, 사용자 프로그램 함수, 프로그램 실행</p>
<br />
<br />

<h3 id="1-컴퓨터-시스템-구조">1) 컴퓨터 시스템 구조</h3>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/f640aa30-706c-47eb-a5c8-9c84f4efde46/image.png" /></p>
<ul>
<li><p><strong>CPU 스케줄링</strong>: 코어가 하나라면 한 번에 하나의 프로세스만 실행 가능함
언제 어떤 프로세스에 할당할지 결정하는 작업
주어진 시간 안에 많은 일을 하게 응답 시간은 짧은 것이 목표</p>
</li>
<li><p><strong>Memory 관리</strong>: 각각의 독립된 메모리 공간을 어떻게 분배하고 관리할 것인지</p>
</li>
<li><p><strong>디스크 파일 관리</strong>: 데이터 저장, 검색, 공유하는데 필요한 파일 시스템을 효과적으로 사용하기 위함, 디스크 스케줄링</p>
</li>
<li><p><strong>입출력 관리</strong>: CPU와 정보를 어떻게 주고받을지, 인터럽트</p>
</li>
</ul>
<br />
<br />
<br />
<br />

<h3 id="1-1-mode-bit">1-1) Mode bit</h3>
<ul>
<li><strong>mode bit 0</strong> : 모니터 모드(=커널 모드, 시스템 모드) , 모든 인터럽트 사용 가능, OS 코드 수행, 보안을 해칠 수 있는 중요한 명령어 사용, interrupt나 exception 발생시 하드웨어가 mode bit을 0으로 바꿈</li>
<li><strong>mode bit 1</strong> : 사용자 모드, 사용자 프로그램 수행, 한정적인 인터럽트 사용 가능<br />
<br />

</li>
</ul>
<h3 id="1-2-timer-interrupt">1-2) Timer Interrupt</h3>
<p>타이머 설정을 해놓음으로써 특정 프로그램이 CPU를 독점하는 것을 막음</p>
<p>ex) 사용자 프로그램이 무한루프를 도는 경우</p>
<br />
<br />
<br />

<h3 id="1-3-io-device-controller">1-3) I/O Device Controller</h3>
<ul>
<li>I/O 장치 유형 관리하는 일종의 작은 CPU</li>
<li>제어정보를 위한 레지스터</li>
<li>데이터를 담은 로컬 버퍼를 가짐</li>
<li>요청이 끝났음을 알려주기 위함<br />
<br />

</li>
</ul>
<h3 id="1-4-io의-수행">1-4) I/O의 수행</h3>
<p>모든 입출력 명령은 mode bit이 0(시스템 모드)일 때 가능
<br /></p>
<p>🤨 사용자 프로그램에서의 I/O ??
<strong><span style="color: blue;">시스템 콜</span></strong>: 사용자 프로그램이 OS에게 I/O 요청을 하는 것.
특정 프로그램 내에서 메소드 호출, 메모리 주소를 가져오는 것이랑 다름</p>
<p>즉, A프로그램에서 OS로 직접 주소 점프를 할 수 없으므로 시스템 콜 사용</p>
<br />
<br />
<br />
<br />

<h3 id="1-5-interrupt">1-5) Interrupt</h3>
<ul>
<li><strong>Intterupt</strong>: 일꾼 개념의 하드웨어(controller)들이 CPU에게 정보교신을 위해 걸어줄 수 있다</li>
<li><strong>Trap</strong>: 사용자 프로그램이 직접 처리 못하고 OS에게 대신 요청해야 하는 상황에 걸 수 있다
e.g. Exception, System call</li>
</ul>
<ol>
<li>Trap을 사용하여 인터럽트 벡터의 특정위치로 이동</li>
<li>제어권이 인터럽트 벡터가 가리키는 '인터럽트 서비스 루틴'으로 이동</li>
<li>(올바른 요청만) I/O 수행</li>
<li>I/O 완료시 제어권을 시스템콜 다음 명령으로 옮김</li>
<li>하드웨어 인터럽트 작동 (I/O controller가 요청 완료 알림)</li>
</ol>
<ul>
<li><p>타이머 인터럽트, 키보드 인터럽트... 종류마다 해야할 일이 다름</p>
</li>
<li><p>인터럽트 벡터: 해당 인터럽트 처리 루틴 주소를 갖고있음
인터럽트 처리 루틴: 해당 인터럽트를 처리하는 커널 함수</p>
</li>
</ul>
<br />
<br />
<br />
<br />

<h3 id="1-6-dmadirect-memory-access-controller">1-6) DMA(Direct Memory Access) Controller</h3>
<p><strong>DMA Controller</strong> : I/O Device 같은 장치의 모든 인터럽트를 CPU가 매번 작업하기엔 오버헤드가 크기 때문에 DMA Controller가 대신 Local Buffer의 내용을 메모리로 복사해줌</p>
<p>메모리에 접근할 수 있는 것은 CPU뿐인데, 예외적으로 DMA도 접근 가능하게 함으로써 CPU 효율을 높임</p>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

<h3 id="2-synchronousasynchronous-io">2) Synchronous/Asynchronous I/O</h3>
<ul>
<li><p><strong><span style="color: red;">Synchronous</span></strong>: I/O 요청 후 입출력 작업이 완료 후에야 제어가 사용자 프로그램으로 넘어감. 작업이 끝나기 전에 다른 명령을 수행할 수 없음 </p>
</li>
<li><p><em>구현1*</em>: I/O가 끝날 때까지 CPU 낭비 시킴, 매 시점 하나의  I/O만 수행</p>
</li>
<li><p><em>구현2*</em>: I/O가 끝날 때까지 해당 프로그램에서 CPU를 뺏음, 던져놓고 CPU를 다른 프로그램에 넘김</p>
<blockquote>
<p>ex) A 프로그램이 명령을 수행하다가 입출력 요청을 하게 되면, A에게 CPU를 빼앗아 다른 프로그램(B)에 CPU를 할당하게 된다. A의 입출력이 완료될 때까지 A에게는 CPU를 할당하지 않음</p>
</blockquote>
</li>
<li><p><strong><span style="color: blue;">Asynchronous</span></strong>: I/O 요청 후에 연산이 끝나기를 기다리지 않고 CPU 제어권이 다시 사용자 프로그램에 즉시 넘어감
작업이 끝나기 전에 다른 명령을 수행할 수 있음</p>
</li>
</ul>
<p>※ 두 경우 모두 I/O 완료는 Interrupt로 알려준다</p>
<br />

<blockquote>
<p><strong>* 헷갈리니까 다시 정리하면 *</strong>
동기식은 A프로그램에서 입출력 연산 요청 후, 사용하지 않는 CPU를 B프로그램에 CPU를 할당할 수 있다. (A프로그램은 입출력 연산이 끝날 때까지 어떤 작업도 할 수 없기 때문)
비동기식은 A프로그램에서 입출력 연산을 요청하고나서 바로 다음 instruction을 수행할 수 있다(A프로그램 내에서)</p>
</blockquote>
 <br />
<br />
<br />
<br />
<br />
<br />



<h3 id="3-memory-mapped-io">3) Memory Mapped I/O</h3>
<p>: CPU가 입출력 장치에 접근할 때, 입출력과 메모리 주소 공간을 분리하지 않고 하나의 메모리 공간으로 취급하여 배치하는 방식.(메모리 일부 공간을 I/O포트에 할당)</p>
<p>따라서 CPU는 파일을 메모리에서 접근할 수 있다. Syetem call을 하지 않고도 메모리에 data를 읽고 쓰는 것처럼 사용 가능</p>
<p>주로 RISC, 임베디드 시스템에서 사용</p>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/0997b0e8-93a3-4245-a774-58c18cad3c15/image.png" /></p>
<p><a href="https://www.baeldung.com/cs/memory-mapped-vs-isolated-io">링크텍스트</a> </p>
<br />
<br />
<br />
<br />
<br />
<br />


<h3 id="4-저장장치-계증구조">4) 저장장치 계증구조</h3>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/a515ffd0-098b-4a7d-89fe-8b1af67bf109/image.png" />
<a href="https://chogyujin.github.io/2019/03/26/2.8-%EC%A0%80%EC%9E%A5-%EC%9E%A5%EC%B9%98%EC%9D%98-%EA%B3%84%EC%B8%B5-%EA%B5%AC%EC%A1%B0/">링크텍스트</a></p>
<blockquote>
<p><strong>캐시(Cache)</strong>: 밑에서부터(Disk) 읽어온 데이터 재요청이 들어오면, 이미 읽어온 데이터를 cache memory에 복사해두었다가 바로 읽어올 수 있음</p>
</blockquote>
<p>ex) 웹 캐시 </p>
<p><strong>브라우저 캐시</strong>: 웹 페이지에 접속할 때, 자원을 하드디스크나 메모리에 캐싱해 뒀다가 다음 번에 다시 접속할 때 재활용
<strong>응답 캐시</strong>: 웹 서버, 동적 웹 페이지라 할지라도 매번 내용이 바뀌지 않는 경우가 많으므로, 서버에서 생성한 HTML을 캐싱해뒀다가 다음 번 요청 때 재활용
<strong>프록시 캐시</strong>: 클라이언트에서 자주 요청 받는 내용은 웹 서버로 전달하지 않고 웹 서버 앞단의 프록시 서버에 캐싱해둔 데이터를 바로 제공</p>
<br />
<br />
<br />
<br />
<br />
<br />


<h3 id="5-프로그램-실행메모리-load">5) 프로그램 실행(메모리 load)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/ca8747ba-6bd2-4b82-8094-c20f6e193dde/image.png" /></p>
<p>프로그램은 실행파일 형태로 비휘발성 하드디스크에 저장되어 있다.
파일 시스템의 실행 파일을 실행 시킬 때는 메모리에 올라가 실행되는데,
물리적인 방법으로 메모리에 바로 올라가는 것이 아니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/6a444e22-0b9c-4ff3-9816-1ec7965d8a21/image.png" /></p>
<p>다음처럼 Virtual memory의 형태로 주소 공간이 형성된다.</p>
<blockquote>
<p><strong>Stack</strong> : 함수 구조의 code를 호출하거나 리턴할 때 데이터를 쌓았다가 꺼내는 용도
<strong>Data</strong>: 프로그램이 사용하는 자료구조를 담음
<strong>Code</strong>: CPU에서 실행할 기계어 코드를 담음
주소 공간의 내용을 Physical memory(물리적 메모리) 공간에 올려서 실행시킴</p>
</blockquote>
<p>하지만 전부 올리는 것이 아닌 그때 그때 필요한 부분만 부분적으로 올리고, 당장 필요하지 않은 내용은 Swap area 디스크 공간에 옮겨둔다.</p>
<blockquote>
<p><strong>swap memory</strong>: RAM이 다 찼을 때 잘 사용하지 않는 페이지들을 옮겨두는 disk 공간 (연장 공간), 하드 디스크에 위치하기 때문에 RAM보다 느림, 휘발성 메모리</p>
</blockquote>
<br />
<br />
<br />
<br />
<br />
<br />

<h3 id="6-커널-주소-공간의-내용">6) 커널 주소 공간의 내용</h3>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/3c5a796d-514c-4cca-b9b2-e2c20fd37f23/image.png" /></p>
<br />
<br />
<br />
<br />
<br />
<br />


<h3 id="7-사용자-프로그램이-사용하는-함수">7) 사용자 프로그램이 사용하는 함수</h3>
<ul>
<li><strong>사용자 정의 함수</strong>: 내가 프로그램에서 직접 작성한 함수</li>
<li><strong>라이브러리 함수</strong>: 누군가 정의해놓은 것을 가져다 쓴 함수</li>
<li><strong>커널 함수</strong>: 운영체제 프로그램의 함수(내 프로그램 안에 있지 않고, 커널 코드 안에 존재)</li>
</ul>
<br />
<br />
<br />
<br />


<h3 id="8-프로그램-실행">8) 프로그램 실행</h3>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/1f165cff-6a92-4311-966d-32d69139a378/image.png" /></p>