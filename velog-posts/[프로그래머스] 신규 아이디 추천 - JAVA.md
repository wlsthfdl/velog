<p><a href="https://school.programmers.co.kr/learn/courses/30/lessons/72410">프로그래머스 문제</a></p>
<br />
<br />

<p>스텝 순서대로 차곡차곡 해주면 된다. </p>
<h3 id="💻-코드">💻 코드</h3>
<pre><code class="language-java">class Solution {
    public String solution(String new_id) {

        //step1
        String answer = new_id.toLowerCase();

        //step2
        answer = answer.replaceAll(&quot;[^a-z0-9-_.]&quot;, &quot;&quot;);

        //step3
        while(answer.contains(&quot;..&quot;)){
            answer = answer.replace(&quot;..&quot;, &quot;.&quot;);
        }

        //step4
        if(answer.charAt(0) == '.'){
            answer = answer.substring(1);
        }
        if(answer.length() &gt; 0 &amp;&amp; answer.charAt(answer.length()-1) == '.'){
            answer = answer.substring(0, answer.length()-1);
        }

        //step5
        if(answer.length() == 0)    answer = &quot;a&quot;;

        //step6
        if(answer.length()&gt;15){
            answer = answer.substring(0, 15);
            //step5 마지막 문자가 '.'일 때
            if(answer.charAt(answer.length()-1) == '.'){
                answer = answer.substring(0, answer.length()-1);
            }
        }

        //step7
        if(answer.length() &lt; 3){
            char last = answer.charAt(answer.length()-1);
            while(answer.length() &lt; 3){
                answer += last;
            }
        }

        return answer;
    }
}</code></pre>
<p><br /><br /></p>
<h3 id="🤨🔎">🤨🔎</h3>
<blockquote>
<p>정규표현식에 대해 다시 한 번 공부하는 계기가 됐다.</p>
</blockquote>