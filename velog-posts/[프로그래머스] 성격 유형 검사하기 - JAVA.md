<p><a href="https://school.programmers.co.kr/learn/courses/30/lessons/118666">https://school.programmers.co.kr/learn/courses/30/lessons/118666</a></p>
<p>다 썼는데 날아갓다
하.........................................^^</p>
<p>왜이래 정말
<br /></p>
<blockquote>
<h4 id="풀이방법">풀이방법</h4>
</blockquote>
<ul>
<li>map 초기화</li>
<li>survey 별로 key, value값 구해서 저장</li>
<li>type(T/R, C/F, J/M, A/N)을 돌면서 더 큰 value를 가진 type을 StringBuilder에 저장</li>
</ul>
<br />
<br />

<h3 id="🤓-코드">🤓 코드</h3>
<pre><code class="language-java">import java.util.*;
class Solution {
    public String solution(String[] survey, int[] choices) {

        char[] type = {'R', 'T', 'C', 'F', 'J', 'M', 'A', 'N'};

        HashMap&lt;Character, Integer&gt; map = new HashMap&lt;&gt;();

        for (int i = 0; i &lt; type.length; i++) {
            map.put(type[i], 0);
        }


        for(int i = 0; i&lt; survey.length; i++){
            int score = choices[i];

            if(score &gt; 0 &amp;&amp; score &lt; 4){
                char ch = survey[i].charAt(0);
                map.put(ch, map.get(ch) + 4 - score);
            }else if(score &gt; 4){
                char ch = survey[i].charAt(1);
                map.put(ch, map.get(ch) + score - 4);            
            }
        }


        StringBuilder sb = new StringBuilder();

        for(int i=0; i&lt;type.length; i+=2){
            char left = type[i];
            char right = type[i+1];

            if(map.get(left) &gt;= map.get(right)){
                sb.append(left);
            }else{
                sb.append(right);
            }
        }

        return sb.toString();
    }
}</code></pre>
<br />

<blockquote>
<h4 id="고찰">고찰</h4>
<p>마지막 for문을 위해 초반에 map을 초기화 해줘야 한다.
그렇지 않으면 NullPointException이 🤷‍♀️</p>
</blockquote>
<p>흥.</p>