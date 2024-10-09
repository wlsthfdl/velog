<p><a href="https://school.programmers.co.kr/learn/courses/30/lessons/92334?language=java">문제링크</a></p>
<br />
<br />

<blockquote>
<h3 id="🔎🤨-풀이방법">🔎🤨 풀이방법</h3>
</blockquote>
<ol>
<li>HashSet&lt;&gt;을 사용하여 중복제거([신고한 유저, 신고 당한 유저] 쌍이 중복이면 안 됨)</li>
<li>이용자 ID마다 메일을 받은 횟수를 int[] answer로 반환해야 하기 때문에 접근할 수 있도록, HashMap을 사용</li>
</ol>
<p><br /><br /></p>
<h3 id="👉-map의-value로-set-넣기">👉 Map의 Value로 Set 넣기</h3>
<pre><code class="language-java">//키 'id_list[i]에 대한 Set 추가
map.put(id_list[i], new HashSet&lt;&gt;());

...

// 키 'str[1]'의 Set에 'str[0]' 값 추가
map.get(str[1]).add(str[0]);
</code></pre>
<br />

<h3 id="👉-map의-결과">👉 map의 결과</h3>
<p>**&quot;신고 당한 유저&quot; : [&quot;신고한 유저1&quot;, &quot;신고한 유저2&quot;, ...]
**</p>
<pre><code class="language-java">HashMap&lt;String, HashSet&lt;String&gt;&gt; map = new HashMap&lt;&gt;();

...

map = {&quot;muzi&quot;:[&quot;apeach&quot;],&quot;neo&quot;:[&quot;muzi&quot;,&quot;frodo&quot;],&quot;frodo&quot;:[&quot;muzi&quot;,&quot;apeach&quot;],&quot;apeach&quot;:[]}</code></pre>
<br />
<br />





<h3 id="💻-코드">💻 코드</h3>
<pre><code class="language-java">import java.util.*;
class Solution {
    public int[] solution(String[] id_list, String[] report, int k) {
        int[] answer = new int[id_list.length];

        // 유저 ID
        HashMap&lt;String, Integer&gt; idmap = new HashMap&lt;&gt;();
        // 신고 당한 유저 : [신고한 유저1 ...] 담을 map
        HashMap&lt;String, HashSet&lt;String&gt;&gt; map = new HashMap&lt;&gt;();

        //init
        for(int i=0; i&lt;id_list.length; i++){
            idmap.put(id_list[i], i);
            map.put(id_list[i], new HashSet&lt;&gt;());
        }

        for(String r : report){
            String str[] = r.split(&quot; &quot;);
            map.get(str[1]).add(str[0]);
        }

        for(int i=0; i&lt;id_list.length; i++){
            HashSet&lt;String&gt; set = map.get(id_list[i]);
            if(set.size() &gt;= k){
                for(String str : set){
                    answer[idmap.get(str)]++;
                }
            }
        }

        return answer;
    }
}</code></pre>