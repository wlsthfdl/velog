<p><a href="https://school.programmers.co.kr/learn/courses/30/lessons/67256">https://school.programmers.co.kr/learn/courses/30/lessons/67256</a></p>
<blockquote>
<h4 id="풀이방법">풀이방법</h4>
</blockquote>
<ul>
<li>손가락은 * , #에서 시작한다. (초기값)</li>
<li>가장 최근 누른 손가락 위치를 저장한다. (left, right 변수)</li>
<li>2, 5, 8, 0 인 경우(0인 경우는 별도처리)
left, right의 위치와 현재 키패드 간의 거리 계산(lDistance, rDistance 변수)
거리가 같을 경우 =&gt; hand</li>
</ul>
<br />


<h3 id="💻코드">💻코드</h3>
<pre><code class="language-java">class Solution {
    public String solution(int[] numbers, String hand) {
        StringBuilder sb = new StringBuilder();

        int left = 10, right = 12;
        for(int num : numbers){
            if(num==1 || num==4 || num==7){
                sb.append(&quot;L&quot;);
                left = num;
            }else if(num==3 || num==6 || num==9){
                sb.append(&quot;R&quot;);
                right = num;
            }else{  // 2, 5, 8, 0인 경우
                if(num==0) num = 11;

                int lDistance = Math.abs(num-left)/3 + Math.abs(num-left)%3;   
                int rDistance = Math.abs(num-right)/3 + Math.abs(num-right)%3;

                if(lDistance &gt; rDistance){
                    sb.append(&quot;R&quot;);
                    right = num;
                }else if(lDistance &lt; rDistance){
                    sb.append(&quot;L&quot;);
                    left = num;
                }else{
                    if(hand.equals(&quot;right&quot;)){
                        sb.append(&quot;R&quot;);
                        right = num;
                    }else{
                        sb.append(&quot;L&quot;);
                        left = num;
                    }
                }

            }
        }

        return sb.toString();
    }
}</code></pre>