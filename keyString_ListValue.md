<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>hashMap_iteration</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><h1 id="leetcode-49-—-group-anagrams">LeetCode 49 — Group Anagrams</h1>
<p>Today I solved an interesting problem on <strong>LeetCode</strong> — <strong>Problem 49: Group Anagrams</strong>.</p>
<p>The core idea of this problem is to <strong>group strings that are anagrams</strong> of each other and return them as a list of lists.</p>
<p>I used an elegant approach where:</p>
<ul>
<li>The <strong>key</strong> is the <strong>sorted version of the string</strong></li>
<li>The <strong>value</strong> is a <strong>list of all strings that match that key</strong></li>
</ul>
<p>This works because all anagrams become identical after sorting their characters.</p>
<hr>
<h2 id="🔑-key-insight">🔑 Key Insight</h2>
<p>If two words are anagrams, their sorted versions are the same.</p>
<p>Example:<br>
“eat” → “aet”<br>
“tea” → “aet”<br>
“tan” → “ant”</p>
<p>So <code>"aet"</code> and <code>"ant"</code> can be used as keys in a map.</p>
<hr>
<p>Time &amp; Space Complexity</p>
<ul>
<li>
<p><strong>Time Complexity:</strong> <code>O(n · k log k)</code><br>
<code>n</code> = number of strings, <code>k</code> = average length of each string</p>
</li>
<li>
<p><strong>Space Complexity:</strong> <code>O(n · k)</code></p>
</li>
</ul>
<h2 id="💻-java-implementation">💻 Java Implementation</h2>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">class</span> <span class="token class-name">Solution</span> <span class="token punctuation">{</span>
    <span class="token keyword">public</span> List<span class="token operator">&lt;</span>List<span class="token operator">&lt;</span>String<span class="token operator">&gt;&gt;</span> <span class="token function">groupAnagrams</span><span class="token punctuation">(</span>String<span class="token punctuation">[</span><span class="token punctuation">]</span> strs<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        Map<span class="token operator">&lt;</span>String<span class="token punctuation">,</span> List<span class="token operator">&lt;</span>String<span class="token operator">&gt;&gt;</span> map <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">HashMap</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        
        <span class="token keyword">for</span> <span class="token punctuation">(</span>String word <span class="token operator">:</span> strs<span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">char</span><span class="token punctuation">[</span><span class="token punctuation">]</span> chars <span class="token operator">=</span> word<span class="token punctuation">.</span><span class="token function">toCharArray</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            Arrays<span class="token punctuation">.</span><span class="token function">sort</span><span class="token punctuation">(</span>chars<span class="token punctuation">)</span><span class="token punctuation">;</span>
            String sortedWord <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">String</span><span class="token punctuation">(</span>chars<span class="token punctuation">)</span><span class="token punctuation">;</span>
            
            <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span>map<span class="token punctuation">.</span><span class="token function">containsKey</span><span class="token punctuation">(</span>sortedWord<span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
                map<span class="token punctuation">.</span><span class="token function">put</span><span class="token punctuation">(</span>sortedWord<span class="token punctuation">,</span> <span class="token keyword">new</span> <span class="token class-name">ArrayList</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span>
            
            map<span class="token punctuation">.</span><span class="token function">get</span><span class="token punctuation">(</span>sortedWord<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span>word<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        
        <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token class-name">ArrayList</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span>map<span class="token punctuation">.</span><span class="token function">values</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>



</code></pre>
</div>
</body>

</html>
