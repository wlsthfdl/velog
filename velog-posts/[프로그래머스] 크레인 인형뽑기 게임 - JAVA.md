<blockquote>
<p>풀이방법</p>
</blockquote>
<ol>
<li>moves의 길이만큼 반복, moves[i]-1 값이 열이 된다.</li>
<li>board의 길이만큼 돌면서, 해당 열 몇 번째 행에 꺼낼 인형이 있는지 확인 
즉, 0행부터 내려오면서 검사하고, 0이 아닌 숫자가 나올 시 break를 통해 탐색을 멈춘다.</li>
<li>Stack을 이용하여 peek값과 격자에서 꺼낸 인형값을 비교</li>
</ol>
<br />
<br />

<h3 id="💻코드">💻코드</h3>
<pre><code class="language-java">import java.util.*;
class Solution {
    public int solution(int[][] board, int[] moves) {
        int answer = 0;

        Stack&lt;Integer&gt; stack = new Stack&lt;&gt;();

        for(int i:moves){
            i -= 1;        //크레인 위치는 1번부터 시작이기 때문에
            for(int j=0; j&lt;board.length; j++){
                if(board[j][i] != 0){
                    if(stack.size()&gt;0 &amp;&amp; stack.peek() == board[j][i]){
                        stack.pop();
                        answer+=2;
                    }else{
                        stack.push(board[j][i]);
                    }
                    board[j][i] = 0;        //뽑힌 인형은 0으로 바꿔줘야 또 쓰이지 않음
                    break;        //가장 위에 있는 인형만 뽑아야함
                }
            }
        } 

        return answer;
    }
}</code></pre>
<blockquote>
<h4 id="고찰">고찰</h4>
<p>처음엔 격자에서 꺼낸 인형 값을 stack에 넣고 전 값과 비교하는 방식을 생각했는데 안 되더라..? <br />
넣지 않고 peek값과 비교한 다음,
같으면 peek값은 꺼내서 지우고, answer에 2 증가
다르면 격자에서 꺼낸 값을 push해줘야 함.<br /></p>
</blockquote>