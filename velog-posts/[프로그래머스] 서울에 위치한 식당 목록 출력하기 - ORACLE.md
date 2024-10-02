<p><a href="https://school.programmers.co.kr/learn/courses/30/lessons/131118">문제 링크</a></p>
<br />
<br />

<h3 id="💻-코드">💻 코드</h3>
<h4 id="☠️-join-풀이-방법">☠️ JOIN 풀이 방법</h4>
<pre><code class="language-sql">SELECT I.REST_ID, I.REST_NAME, I.FOOD_TYPE,    I.FAVORITES, I.ADDRESS,    
       ROUND(AVG(R.REVIEW_SCORE), 2) SCORE
FROM REST_INFO I JOIN REST_REVIEW R
ON I.REST_ID = R.REST_ID 
WHERE I.ADDRESS LIKE '서울%' 
GROUP BY I.REST_ID, I.REST_NAME, I.FOOD_TYPE, I.FAVORITES, I.ADDRESS
ORDER BY 6 DESC, 4 DESC;</code></pre>
<br />

<h4 id="☠️-인라인뷰-풀이-방법">☠️ 인라인뷰 풀이 방법</h4>
<pre><code class="language-sql">SELECT I.REST_ID, I.REST_NAME, I.FOOD_TYPE,    I.FAVORITES, I.ADDRESS, R.SCORE
FROM REST_INFO I 
    (SELECT REST_ID, ROUND(AVG(REVIEW_SCORE),2) AS SCORE
     FROM   REST_REVIEW
     GROUP BY REST_ID) R
WHERE I.REST_ID = R.REST_ID
    AND I.ADDRESS LIKE '서울%' 
ORDER BY 6 DESC, 4 DESC;</code></pre>
<p><br /><br /><br /></p>
<blockquote>
<h3 id="🤨-고찰">🤨 고찰</h3>
<p>'서울특별시~'로 시작되지 않는 서울시도 있음
JOIN을 쓸 경우, SELECT절에 포함된 비집계 열들은 모두 GROUP BY에 포함되어야 함
인라인 뷰를 사용하는 게 더 편하다.</p>
</blockquote>
<p>SQL 마니 잊어버렸다 (┬┬﹏┬┬)</p>