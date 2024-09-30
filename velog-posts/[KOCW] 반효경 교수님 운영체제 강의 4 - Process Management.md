<p>개요: 프로세스 생성 및 종료, 프로세스와 관련한 시스템콜, 프로세스 간 협력, Message Passing, Interprocess communication, CPU and I/O Bursts in Program Execution, CPU-burst Time의 분포, 프로세스의 특성 분류, CPU Scheduler &amp; Dispatcher
<br />
<br />
<br /></p>
<h3 id="1-프로세스-생성">1) 프로세스 생성</h3>
<p>: 부모 프로세스가 자식 프로세스를 생성, 트리(계층형) 구조, 프로세스는 OS 혹은 부모로부터 받는 자원을 필요로 함.
<br /></p>
<p> *<em>자원 공유  *</em></p>
<ul>
<li>부모와 모두 공유</li>
<li>부모와 일부 공유</li>
<li>공유하지 않음<br />

</li>
</ul>
<p>*<em>수행(Execution) *</em></p>
<ul>
<li>부모와 자식이 공존하며 수행하 모델</li>
<li>자식이 종료될 때까지 부모가 기다리는 모델<br />

</li>
</ul>
<p><strong>주소 공간(Address space)</strong></p>
<p>: 자식은 부모의 주소 공간을 복사하고 그 공간에 새로운 프로그램을 올림</p>
<blockquote>
<p>ex) UNIX
 <strong>fork() *<em>: 시스템 콜이 새로운 프로세스를 생성, 부모를 그대로 복사(OS data except PID + binary), 주소공간 할당
 *</em>exec()</strong> : 시스템 콜을 통해 새로운 프로그램을 메모리에 올림
** exit() <strong>: 자식이 부모에게 output data보냄 (via wait), 각종 자원들이 운영체제에 반납됨
 **abort()</strong> : 부모 프로세스가 자식의 수행을 종료시킴 (자식 프로세스가 더이상 필요 없을 때, 자식이 할당 자원의 한계치를 넘어섬, 부모가 종료돠는 경우, 단계적 종료)</p>
</blockquote>
 <br />



<h3 id="🤓-cowcopy-on-write">🤓 COW(Copy-on-write)?</h3>
<p>: fork() 수행하면서 자식 프로세스가 부모 프로세스의 복사본이 되는데, exec()를 수행해 새로운 프로세스를 overwrite하는 과정에서 오버헤드가 발생한다.
 따라서 자식 프로세스에서 수정됨이 발생함에 따라 필요한 부분만 copy 수행하여, 내용이 변경될 때만 새로운 page를 할당해주어 오버헤드를 감소시킴.</p>
<p><br /><br /><br /><br /></p>
<h3 id="2-시스템-콜">2) 시스템 콜</h3>
<h3 id="2-1-fork-시스템-콜">2-1) fork() 시스템 콜</h3>
<pre><code class="language-c">int main() {
    int pid;
    pid = fork();
    if(pid == 0) printf(&quot;\n Hello, I am child!\n&quot;);
    else if(pid &gt; 0) printf(&quot;\n Hello, I am parent!\n&quot;);
}</code></pre>
<ul>
<li>프로세스는 fork() 시스템 콜에의해 생성됨</li>
<li>이 때 생성된 프로세스(자식)은 부모 프로세스의 문맥을 그대로 이어 받아 fork()메소드 이후부터 실행.</li>
</ul>
<br />

<h3 id="2-2-exec-시스템-콜">2-2) exec() 시스템 콜</h3>
<pre><code class="language-c">int main() {
    int pid;
    pid = fork();

    if(pid == 0) {
        printf(&quot;\n Hello, I am child!\n&quot;);
        execlp(&quot;/bin/date&quot;, &quot;/bin/date&quot;, (char *) 0);
    }

    else if(pid &gt; 0) {
        printf(&quot;\n Hello, I am parent!\n&quot;);
    }
}

/* date */
int main() {
    ...
}</code></pre>
<ul>
<li>프로세스는 exec() 시스템 콜을 통해 다른 프로그램을 실행한다. </li>
<li>execlp 시점에서 새로운 시스템으로 바뀌며 date라는 새로운 프로그램으로 덮어쓰고, execlp 이후엔 다시 돌아오지 않음. (이후 코드는 실행 X)<br />

</li>
</ul>
<h3 id="2-3-wait-시스템-콜">2-3) wait() 시스템 콜</h3>
<pre><code class="language-c">int main {
    int childPID;
    S1;

    childPID = fork();

    if(childPID == 0)
        ...
    else {
        wait();
    }

    S2;
}</code></pre>
<ul>
<li>프로세스 A가 wait()를 호출하면 커널은 child가 종료될 때까지 A를 sleep 시킴 (blocked) ==&gt; 자식 프로세스가 종료되면 커널은 A를 깨움(ready)<br />

</li>
</ul>
<blockquote>
<p>e.g) <strong>Linux prompt</strong>
|(shell prompt) Program A 
(엔터 == wait..... , A가 끝나면 B 실행)
|(shell prompt) Program B</p>
</blockquote>
<br />

<h3 id="2-4-exit-시스템-콜">2-4) exit() 시스템 콜</h3>
<ul>
<li>자발적 종료<ul>
<li>마지막 statement 수행 후 exit() 시스템 콜을 통해 이루어짐</li>
<li>명시적으로 적어주지 않아도 묵시적으로 컴파일러가 넣어줌</li>
</ul>
</li>
<li>비자발적 종료<ul>
<li>부모 프로세스가 강제 종료시킴</li>
<li>kill, break</li>
<li>부모가 종료하는 경우(자식들이 먼저 종료됨)</li>
</ul>
</li>
</ul>
<p><br /><br /><br /><br /><br /><br /></p>
<h3 id="3-프로세스-간-협력">3) 프로세스 간 협력</h3>
<ul>
<li>독립적 프로세스: 프로세스는 각자의 주소 공간을 가지고 수행되므로, 원칙적으로 하나의 프로세스는 다른 프로세스 수행에 영향을 미치지 못함</li>
<li>협력 프로세스: 프로세스 협력 매커니즘을 통해 영향을 미칠 수 있음</li>
<li>프로세스 간 협력 매커니즘(IPC)<ul>
<li>메세지 전달(message passing): 커널을 통해 메시지 전달 </li>
<li>주소 공간 공유(shared memory): 서로 다른 프로세스 간에도 일부 주소 공간 공유</li>
</ul>
</li>
</ul>
<blockquote>
<p><strong>Thread</strong>는 
사실상 하나의 프로세스이므로 프로세스 간 협력으로 보기 어렵지만, 동일한 process를 구성하는 Thread들 간에는 주소공간을 공유하므로 협력이 가능</p>
</blockquote>
<p>  <img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/232b6231-1eec-49fd-af2d-f1e8489a7182/image.png" />
<a href="https://woojin.tistory.com/87">링크텍스트</a></p>
<br />

<h3 id="3-1-message-passing">3-1) Message Passing</h3>
<ul>
<li>프로세스 사이에 공유 변수를 일체 사용하지 않고 통신하는 시스템<ul>
<li>Direct Communication : 통신하려는 프로세스의 이름을 명시적으로 표시 </li>
<li>Indirect Communication : Mailbox(또는 Port)를 통해 메시지를 간접 전달</li>
</ul>
</li>
</ul>
<p><br /><br /><br /><br /></p>