<br />

<h3 id="1-cpu-and-io-bursts-in-program-execution">1) CPU and I/O Bursts in Program Execution</h3>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/cadecb41-01dc-4cea-a28e-a3de03993748/image.png" /></p>
<ul>
<li>I/O Bound job : I/O burst가 잦은 프로그램 <ul>
<li>짧은 CPU burst가 많은 수로 존재</li>
</ul>
</li>
<li>CPU Bound job : CPU burst 지속기간이 긴 프로그램<ul>
<li>긴 CPU burst가 적은 수로 존재</li>
</ul>
</li>
<li>여러 종류의 job이 섞여 있으므로 CPU 스케줄링이 필요하다</li>
<li>공평하기보다는 효율적으로 자원을 분배할 필요성<br />
<br />
<br />

</li>
</ul>
<h3 id="2-cpu-schedular--dispatcher">2) CPU Schedular &amp; Dispatcher</h3>
<ul>
<li><p><strong>CPU Schedular</strong></p>
<ul>
<li>ready 상태의 프로세스 중 CPU를 넘겨줄 프로세스를 고른다.</li>
<li>운영체제 안에 코드로 존재함</li>
</ul>
</li>
<li><p><strong>Dispatcher</strong></p>
<ul>
<li>CPU 제어권을 넘기는 역할, 이 과정을 Context Switch라고 함</li>
<li>운영체제 안에 코드로 존재함</li>
</ul>
</li>
<li><p><strong>CPU 스케줄링이 필요한 경우</strong></p>
<ol>
<li>Running → Blocked (eg: I/O 요청하는 시스템 콜)</li>
<li>Running → Ready (eg: 할당시간 만료로 Timer interrupt)</li>
<li>Blocked → Ready (eg: I/O 완료 후 인터럽트)</li>
<li>Terminate</li>
</ol>
<p>2, 3 그 외 모든 스케줄링 → <strong>Preemptive(강제로 빼앗음)</strong>
1, 4 → <strong>Nonpreemptive(자진반납)</strong></p>
<br />
<br />
<br /><br /><br />



</li>
</ul>
<h3 id="3-성능척도scheduling-criteria">3) 성능척도(Scheduling Criteria)</h3>
<p>  : 프로세스의 시작/종료 기준이 아니라 Process가 CPU를 잡고있는 시간 기준</p>
<ul>
<li>CPU 입장<ul>
<li>CPU utilization (이용률)</li>
<li>Throghput (처리량)</li>
</ul>
</li>
<li>프로세스 입장<ul>
<li>Turnaround Time (반환시간)</li>
<li>Waiting Time (대기시간, 선점형일 때, CPU를 뺏기고 기다린 총 시간)</li>
<li>Response Time (응답시간, 최초의 CPU를 얻기까지 기다린 시간)</li>
</ul>
</li>
</ul>
<p><br /><br /><br /><br /><br /></p>
<h3 id="4-scheduling-algorithm">4) Scheduling Algorithm</h3>
<h3 id="4-1-fcfs-first-come-first-served">4-1) FCFS (First-Come First-Served)</h3>
<ul>
<li>nonpreemptive</li>
<li><strong>프로세스 도착 순서대로</strong> CPU 할당</li>
<li>앞에 도착한 프로세스의 사용시간이 긴 경우 ==&gt; 평균 Waiting Time이 길어짐 (Convoy effect)</li>
</ul>
<br />

<h3 id="4-2-sjf-short-job-first">4-2) SJF (Short-Job First)</h3>
<ul>
<li><p>CPU Burst time이 가장 짧은 것 먼저</p>
<ul>
<li>nonpreemptive</li>
<li>preeamptive : 현재 수행 중인 프로세스의 남은 burst time보다 더 짧은 CPU burst time을 가진 새로운 프로세스가 도착하면 CPU 뺏어감
(== <strong>SRTF</strong>: Shortest-Remaining-Time-First)</li>
</ul>
</li>
<li><p>Optimal하다. Minimum average waiting time을 보장</p>
</li>
</ul>
<ul>
<li>단점: Starvation, Long Process가 영원히 실행되지 않을 수도 있음
프로그램의 정확한 사용시간을 미리 예측할 수 없음</li>
</ul>
<br />

<h3 id="4-3-priority-schedular">4-3) Priority Schedular</h3>
<ul>
<li>우선순위가 높은 프로세스에게 CPU를 줌<ul>
<li>nonpreemptive</li>
<li>preemptive</li>
</ul>
</li>
<li>우선순위는 점수로 나타내며, 작을수록 우선순위가 높음</li>
<li>SJF도 우선순위 스케줄링의 일종</li>
<li>단점: Starvation</li>
<li>해결방법: Aging (오래 기다리게 되면 우선순위를 높여줌)</li>
</ul>
<br />

<h3 id="4-4-rr-round-robin">4-4) RR (Round Robin)</h3>
<p>: <strong>현재의 운영체제가 채택한 방법</strong></p>
<ul>
<li>각 프로세스는 동일한 할당시간(q)를 가짐<ul>
<li>일반적으로 10~100ms</li>
</ul>
</li>
<li>할당시간이 끝나면 프로세스는 선점(preempted) 당하고, ready queue 제일 뒤로 가서 다시 줄을 선다</li>
<li>큐에 n개의 프로세스가 있고, 할당시간(Time Quantum)이 q라고 하면, 각 프로세스는 q time unit 단위로 CPU 시간의 1/n을 얻는다. </li>
<li><em>적어도 (n-1)</em>q time unit을 기다리면 한 번은 본인 차례가 온다** 
즉, response time이 짧음</li>
<li>q가 크면 ==&gt; FCFS , q가 작으면 ==&gt; context switch가 빈번해져 overhead</li>
<li>SJF보다 Average wait time은 길어질 수 있지만 response time은 더 짧음</li>
</ul>
<br />
<br />
<br />
<br />

<h3 id="5-multilevel-queue">5) Multilevel Queue</h3>