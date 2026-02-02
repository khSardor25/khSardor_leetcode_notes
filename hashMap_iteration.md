<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>hashMap_iteration</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__left">
    <div class="stackedit__toc">
      
<ul>
<li><a href="#🧩-leetcode-12-—-integer-to-roman">🧩 LeetCode 12 — Integer to Roman</a>
<ul>
<li><a href="#🔁-iterating-through-a-map-using-entryset">🔁 Iterating Through a Map Using entrySet()</a></li>
</ul>
</li>
</ul>

    </div>
  </div>
  <div class="stackedit__right">
    <div class="stackedit__html">
      <h1 id="🧩-leetcode-12-—-integer-to-roman">🧩 LeetCode 12 — Integer to Roman</h1>
<p>Today I solved an interesting problem on <strong>LeetCode</strong>:<br>
<strong>Integer → Roman (Problem #12)</strong>.</p>
<p>One very useful trick I discovered was iterating through a <code>HashMap</code> (or <code>LinkedHashMap</code>) using <code>entrySet()</code>.</p>
<p>This approach lets you access <strong>both keys and values</strong> at the same time — which is perfect for greedy algorithms like Roman numeral conversion.</p>
<hr>
<h2 id="🔁-iterating-through-a-map-using-entryset">🔁 Iterating Through a Map Using <code>entrySet()</code></h2>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">for</span> <span class="token punctuation">(</span>Map<span class="token punctuation">.</span>Entry<span class="token operator">&lt;</span>Integer<span class="token punctuation">,</span> String<span class="token operator">&gt;</span> entry <span class="token operator">:</span> myMap<span class="token punctuation">.</span><span class="token function">entrySet</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">int</span> key <span class="token operator">=</span> entry<span class="token punctuation">.</span><span class="token function">getKey</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    String str <span class="token operator">=</span> entry<span class="token punctuation">.</span><span class="token function">getValue</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

    System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"Key: "</span> <span class="token operator">+</span> key <span class="token operator">+</span> <span class="token string">" Value: "</span> <span class="token operator">+</span> str<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

</code></pre>

    </div>
  </div>
</body>

</html>
