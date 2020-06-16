---
id: 678
title: Dict-based Find and Replace Deluxe
date: 2018-03-12
author: admin
layout: revision
guid: http://pythoninthewyld.com/2018/03/12/674-revision-v1/
permalink: /2018/03/12/674-revision-v1/
---
<div>
  Using a dict to perform find and replace tasks makes a lot of sense; they're simple to implement and they allow us to easily store the target with our desired replacement in one spot. There are a few hidden traps to keep be aware of, but they're easily avoided and we can be back on track reaping the benefits with just a little forethought.
</div>

<div>
  <label for="embed-it-edit-class"><b> <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <h1 id="Find-and-Replace-Deluxe:">
              Find and Replace Deluxe:<a class="anchor-link" href="#Find-and-Replace-Deluxe:">&#182;</a>
            </h1>
            
            <h2 id="How-to-use-a-Python-dict-for-find/replace-functions">
              How to use a Python dict for find/replace functions<a class="anchor-link" href="#How-to-use-a-Python-dict-for-find/replace-functions">&#182;</a>
            </h2>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <p>
              We're going to go through several examples of find-and-replace tasks of varying complexity. We'll also find some potential hiccups and how to avoid them. We're going to use a simple string that is a coherent message if the code works and is hard to read if it isn't to see if our efforts are working.
            </p>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <h3 id="Simple-character-character-substitution">
              Simple character-character substitution<a class="anchor-link" href="#Simple-character-character-substitution">&#182;</a>
            </h3>
            
            <p>
              Replacing one character with another is pretty straightforward using a function. This function takes the string and the dict as arguments, iterates through them, and makes the replacements. You'll notice it has an "if" statement. This is to make sure that the item exists in our dict or else we get a keyError. We can't replace something will the right pair in the dict if the item isn't in the dict, and, if you think about it, that's what we're trying to do if we iterate over every letter and look it up in the dict regardless of whether or not it's there.
            </p>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <p>
              Note: I'm going to comment every line on this one to make sure we're on the same page as this function will serve as the basis of all the ones coming after it. After that, I'll just highlight what is different about the function.
            </p>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing code_cell rendered">
        <div class="input">
          <div class="prompt input_prompt">
            In&nbsp;[16]:
          </div>
          
          <div class="inner_cell">
            <div class="input_area">
              <div class=" highlight hl-ipython3">
                <pre><span></span><span class="c1"># here is our target string, contaminated with "X"s</span>
<span class="n">s</span> <span class="o">=</span> <span class="s2">"HEREXISXAXSAMPLEXSTRING"</span>

<span class="c1"># dictionary pairs "X" with "-"</span>
<span class="n">d</span> <span class="o">=</span> <span class="p">{</span><span class="s2">"X"</span><span class="p">:</span><span class="s2">"-"</span><span class="p">}</span>

<span class="c1"># define a functions that takes a string and a dict</span>
<span class="k">def</span> <span class="nf">find_replace</span><span class="p">(</span><span class="n">string</span><span class="p">,</span> <span class="n">dictionary</span><span class="p">):</span>
    <span class="c1"># is the item in the dict?</span>
    <span class="k">for</span> <span class="n">item</span> <span class="ow">in</span> <span class="n">string</span><span class="p">:</span>
        <span class="c1"># iterate by keys</span>
        <span class="k">if</span> <span class="n">item</span> <span class="ow">in</span> <span class="n">dictionary</span><span class="o">.</span><span class="n">keys</span><span class="p">():</span>
            <span class="c1"># look up and replace</span>
            <span class="n">string</span> <span class="o">=</span> <span class="n">string</span><span class="o">.</span><span class="n">replace</span><span class="p">(</span><span class="n">item</span><span class="p">,</span> <span class="n">dictionary</span><span class="p">[</span><span class="n">item</span><span class="p">])</span>
    <span class="c1"># return updated string</span>
    <span class="k">return</span> <span class="n">string</span>

<span class="c1"># call the funciton</span>
<span class="n">find_replace</span><span class="p">(</span><span class="n">s</span><span class="p">,</span><span class="n">d</span><span class="p">)</span>
</pre>
              </div>
            </div>
          </div>
        </div>
        
        <div class="output_wrapper">
          <div class="output">
            <div class="output_area">
              <div class="prompt output_prompt">
                Out[16]:
              </div>
              
              <div class="output_text output_subarea output_execute_result">
                <pre>&#39;HERE-IS-A-SAMPLE-STRING&#39;</pre>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <p>
              We can see that all the "X"s have been replaced by "-", their paired value.
            </p>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <h3 id="Replacing-multi-character-values">
              Replacing multi-character values<a class="anchor-link" href="#Replacing-multi-character-values">&#182;</a>
            </h3>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <p>
              This follows the same basic pattern, but uses a simple regex function. We will get rid of "ABC"s instead of "X"s. We import the re library and modify our string and dict for the test.
            </p>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing code_cell rendered">
        <div class="input">
          <div class="prompt input_prompt">
            In&nbsp;[17]:
          </div>
          
          <div class="inner_cell">
            <div class="input_area">
              <div class=" highlight hl-ipython3">
                <pre><span></span><span class="kn">import</span> <span class="nn">re</span>

<span class="n">s</span> <span class="o">=</span> <span class="s2">"HEREABCISABCAABCSAMPLEABCSTRING"</span>

<span class="n">d</span> <span class="o">=</span> <span class="p">{</span><span class="s2">"ABC"</span><span class="p">:</span><span class="s2">"-"</span><span class="p">}</span>

<span class="k">def</span> <span class="nf">find_replace_multi</span><span class="p">(</span><span class="n">string</span><span class="p">,</span> <span class="n">dictionary</span><span class="p">):</span>
    <span class="k">for</span> <span class="n">item</span> <span class="ow">in</span> <span class="n">dictionary</span><span class="o">.</span><span class="n">keys</span><span class="p">():</span>
        <span class="c1"># sub item for item&#39;s paired value in string</span>
        <span class="n">string</span> <span class="o">=</span> <span class="n">re</span><span class="o">.</span><span class="n">sub</span><span class="p">(</span><span class="n">item</span><span class="p">,</span> <span class="n">dictionary</span><span class="p">[</span><span class="n">item</span><span class="p">],</span> <span class="n">string</span><span class="p">)</span>
    <span class="k">return</span> <span class="n">string</span>

<span class="n">find_replace_multi</span><span class="p">(</span><span class="n">s</span><span class="p">,</span> <span class="n">d</span><span class="p">)</span>
</pre>
              </div>
            </div>
          </div>
        </div>
        
        <div class="output_wrapper">
          <div class="output">
            <div class="output_area">
              <div class="prompt output_prompt">
                Out[17]:
              </div>
              
              <div class="output_text output_subarea output_execute_result">
                <pre>&#39;HERE-IS-A-SAMPLE-STRING&#39;</pre>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <h3 id="Replacing-single-and-multi-character-patterns...-oh-wait,-crap....">
              Replacing single and multi character patterns... oh wait, crap....<a class="anchor-link" href="#Replacing-single-and-multi-character-patterns...-oh-wait,-crap....">&#182;</a>
            </h3>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <p>
              There is a final kink in this however. What would happen if one of the single character values we wanted to replace occurs within the multi-character string?
            </p>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing code_cell rendered">
        <div class="input">
          <div class="prompt input_prompt">
            In&nbsp;[18]:
          </div>
          
          <div class="inner_cell">
            <div class="input_area">
              <div class=" highlight hl-ipython3">
                <pre><span></span><span class="c1"># the middle "ABC" has been replaced with just an "C"</span>
<span class="n">s</span> <span class="o">=</span> <span class="s2">"HEREABCISABCACSAMPLEABCSTRING"</span>

<span class="c1"># ...which we see </span>
<span class="n">find_replace_multi</span><span class="p">(</span><span class="n">s</span><span class="p">,</span><span class="n">d</span><span class="p">)</span>
</pre>
              </div>
            </div>
          </div>
        </div>
        
        <div class="output_wrapper">
          <div class="output">
            <div class="output_area">
              <div class="prompt output_prompt">
                Out[18]:
              </div>
              
              <div class="output_text output_subarea output_execute_result">
                <pre>&#39;HERE-IS-ACSAMPLE-STRING&#39;</pre>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <p>
              Alas! It seems we have a variation. We assumed all the problematic strings were "ABC"s, but one is just a "C". No problem, right? We just update the dictionary to get rid of "C" as well. Not quite. Here is the thing that goes wrong with these types of functions: we don't know what order the substitutions are happening in. So we might remove the "C" from "ABC" (leaving it as just "AB") first thing, then when we look for "ABC"s to sub, there wont be any. Our program would end without doing anything, and we would still have the "AB".
            </p>
            
            <p>
              For another example, imagine we are replacing "Hello" with 1, and "He" with 2. Our string could be "He Said Hello". If "He" gets changed first, we would have "2 Said 2llo". When we go to look for hello? There is no hello.
            </p>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <h3 id="So-what-do-we-do?">
              So what do we do?<a class="anchor-link" href="#So-what-do-we-do?">&#182;</a>
            </h3>
            
            <p>
              My solution for this problem is to make sure we iterate through the dictionary keys from LARGEST by length to SMALLEST by length to ensure that we don't replace any pieces of them by accident. Using the He/Hello example, we substitute the "Hello" first so none of the substrings ("He") can interfere. We can do this by using the sorted() function and using the reverse = True options (it goes smallest to largest by default). Check it.
            </p>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing code_cell rendered">
        <div class="input">
          <div class="prompt input_prompt">
            In&nbsp;[19]:
          </div>
          
          <div class="inner_cell">
            <div class="input_area">
              <div class=" highlight hl-ipython3">
                <pre><span></span><span class="n">s</span> <span class="o">=</span> <span class="s2">"HEREABCISABCACSAMPLEABCSTRING"</span>

<span class="n">d</span> <span class="o">=</span><span class="p">{</span><span class="s2">"C"</span><span class="p">:</span><span class="s2">"-"</span><span class="p">,</span> <span class="s2">"ABC"</span><span class="p">:</span><span class="s2">"-"</span><span class="p">}</span>

<span class="k">def</span> <span class="nf">find_replace_multi_ordered</span><span class="p">(</span><span class="n">string</span><span class="p">,</span> <span class="n">dictionary</span><span class="p">):</span>
    <span class="c1"># sort keys by length, in reverse order</span>
    <span class="k">for</span> <span class="n">item</span> <span class="ow">in</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">dictionary</span><span class="o">.</span><span class="n">keys</span><span class="p">(),</span> <span class="n">key</span> <span class="o">=</span> <span class="nb">len</span><span class="p">,</span> <span class="n">reverse</span> <span class="o">=</span> <span class="kc">True</span><span class="p">):</span>
        <span class="n">string</span> <span class="o">=</span> <span class="n">re</span><span class="o">.</span><span class="n">sub</span><span class="p">(</span><span class="n">item</span><span class="p">,</span> <span class="n">dictionary</span><span class="p">[</span><span class="n">item</span><span class="p">],</span> <span class="n">string</span><span class="p">)</span>
    <span class="k">return</span> <span class="n">string</span>

<span class="n">find_replace_multi_ordered</span><span class="p">(</span><span class="n">s</span><span class="p">,</span> <span class="n">d</span><span class="p">)</span>
</pre>
              </div>
            </div>
          </div>
        </div>
        
        <div class="output_wrapper">
          <div class="output">
            <div class="output_area">
              <div class="prompt output_prompt">
                Out[19]:
              </div>
              
              <div class="output_text output_subarea output_execute_result">
                <pre>&#39;HERE-IS-A-SAMPLE-STRING&#39;</pre>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <p>
              Looks as if we are on the right track. Because we replaced the biggest strings first ("ABC"), and the the smallest ("C"), we ensure the "C" in "ABC" didn't get messed with. I'll write one more test to be sure. To confirm that the largest is going first, and not simply that "ABC" is going before "C", we'll add another value to the dict (the rest of the code stays the same). I'll use "CSAMPLEABC", because the only way for that to be replaced is if it goes before "C" and "ABC" as BOTH of those strings are in it.
            </p>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing code_cell rendered">
        <div class="input">
          <div class="prompt input_prompt">
            In&nbsp;[20]:
          </div>
          
          <div class="inner_cell">
            <div class="input_area">
              <div class=" highlight hl-ipython3">
                <pre><span></span><span class="n">s</span> <span class="o">=</span> <span class="s2">"HEREABCISABCACSAMPLEABCSTRING"</span>

<span class="n">d</span> <span class="o">=</span><span class="p">{</span><span class="s2">"C"</span><span class="p">:</span><span class="s2">"-"</span><span class="p">,</span> <span class="s2">"ABC"</span><span class="p">:</span><span class="s2">"-"</span><span class="p">,</span> <span class="s2">"CSAMPLEABC"</span><span class="p">:</span><span class="s2">"-:)-"</span><span class="p">}</span>

<span class="k">def</span> <span class="nf">find_replace_multi_ordered</span><span class="p">(</span><span class="n">string</span><span class="p">,</span> <span class="n">dictionary</span><span class="p">):</span>
    <span class="c1"># sort keys by length, in reverse order</span>
    <span class="k">for</span> <span class="n">item</span> <span class="ow">in</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">dictionary</span><span class="o">.</span><span class="n">keys</span><span class="p">(),</span> <span class="n">key</span> <span class="o">=</span> <span class="nb">len</span><span class="p">,</span> <span class="n">reverse</span> <span class="o">=</span> <span class="kc">True</span><span class="p">):</span>
        <span class="n">string</span> <span class="o">=</span> <span class="n">re</span><span class="o">.</span><span class="n">sub</span><span class="p">(</span><span class="n">item</span><span class="p">,</span> <span class="n">dictionary</span><span class="p">[</span><span class="n">item</span><span class="p">],</span> <span class="n">string</span><span class="p">)</span>
    <span class="k">return</span> <span class="n">string</span>

<span class="n">find_replace_multi_ordered</span><span class="p">(</span><span class="n">s</span><span class="p">,</span> <span class="n">d</span><span class="p">)</span>
</pre>
              </div>
            </div>
          </div>
        </div>
        
        <div class="output_wrapper">
          <div class="output">
            <div class="output_area">
              <div class="prompt output_prompt">
                Out[20]:
              </div>
              
              <div class="output_text output_subarea output_execute_result">
                <pre>&#39;HERE-IS-A-:)-STRING&#39;</pre>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <p>
              And there we have it! Our final function. It's worth noting that, while I made the initial character-character find-and-replace function to work us up to this one, we final function will work for simple character-character substitutions too, so we only need the one, final version for all the tasks here. I'd advise doing so because it has error avoidance with the iteration and the "if" statement.
            </p>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <h3 id="If-you're-the-type-to-stick-around-after-the-credits...">
              If you're the type to stick around after the credits...<a class="anchor-link" href="#If-you're-the-type-to-stick-around-after-the-credits...">&#182;</a>
            </h3>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <p>
              ...here is a bonus and final note of caution:
            </p>
            
            <p>
              What goes wrong if we don't use the new version?
            </p>
          </div>
        </div>
      </div>
      
      <div class="cell border-box-sizing text_cell rendered">
        <div class="prompt input_prompt">
        </div>
        
        <div class="inner_cell">
          <div class="text_cell_render border-box-sizing rendered_html">
            <p>
              This version of the function avoids situations that seem fine but could cause problems. Python dictionaries are unordered. There is, generally, no reason to store the items in order because you look up things up with keys, not an index like an array. Note that the order stays the same, it's just generated with no concern for sequence.
            </p>
            
            <p>
              If you're using a dictionary then, it's thus possible to "accidentally" find and replace in the "right" order. This will produce the exact results you are looking for but might not in the future if the dictionary is ever updated. For example, if "ABC" happened to be replaced before "A", it would look like things were fine, but the next time you run the code from scratch they might not be.
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>  </b>
  
  <br /> </label>
</div>