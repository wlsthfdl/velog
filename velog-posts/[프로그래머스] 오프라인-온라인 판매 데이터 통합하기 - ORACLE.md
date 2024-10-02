<p><a href="https://school.programmers.co.kr/learn/courses/30/lessons/131537">문제 링크</a></p>
<br />
<br />

<h2 id="💻-코드">💻 코드</h2>
<pre><code class="language-sql">SELECT TO_CHAR(SALES_DATE,'YYYY-MM-DD') AS SALES_DATE, PRODUCT_ID, USER_ID, SALES_AMOUNT
FROM ONLINE_SALE
WHERE TO_CHAR(SALES_DATE, 'YY-MM') = '22-03'

UNION ALL

SELECT TO_CHAR(SALES_DATE,'YYYY-MM-DD') AS SALES_DATE, PRODUCT_ID, NULL AS USER_ID, SALES_AMOUNT
FROM OFFLINE_SALE
WHERE TO_CHAR(SALES_DATE, 'YY-MM') = '22-03'
ORDER BY 1,2,3;</code></pre>
<br />
<br />
<br />

<h3 id="🤨-join과-union-">🤨 JOIN과 UNION ?</h3>
<p><img alt="" src="https://velog.velcdn.com/images/wlsthfdl/post/9f9dade1-6f3c-40d9-8e6d-b543ba805327/image.png" />
참고: <a href="https://lyk00331.tistory.com/m/110">https://lyk00331.tistory.com/m/110</a></p>
<ul>
<li>UNION : 하나의 결과 세트만 나타냄</li>
<li>JOIN : 적어도 하나의 속성이 공통인 두 테이블 속성을 결합하고자 할 때 사용<br />
<br />
<br />


</li>
</ul>
<blockquote>
<h4 id="🔎-고찰">🔎 고찰</h4>
<p>FULL OUTER JOIN으로 풀 뻔 했다. 이는 결합연산이라 조인한 결과가 한 행으로 나오지만,
이 문제는 오프라인/온라인마다 각각 별개의 행으로 출력되어야 했기 때문에 UNION을 사용해야 한다. </p>
</blockquote>