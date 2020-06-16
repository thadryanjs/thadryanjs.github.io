---
id: 779
title: 'Closures in Python'
date: 2019-03-28
author: admin
layout: revision
guid: http://pythoninthewyld.com/2019/03/28/778-revision-v1/
permalink: /2019/03/28/778-revision-v1/
---
**<div tabindex="-1" id="notebook" class="border-box-sizing">
  <div class="container" id="notebook-container">
    <div class="cell border-box-sizing text_cell rendered">
      <div class="prompt input_prompt">
      </div>
      
      <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
          <h1 id="Closures-in-Python:">
            Closures in Python:<a class="anchor-link" href="#Closures-in-Python:">&#182;</a>
          </h1>
          
          <h2 id="What-they-are,-and-a-practical-application-for-type-checking-objects">
            What they are, and a practical application for type-checking objects<a class="anchor-link" href="#What-they-are,-and-a-practical-application-for-type-checking-objects">&#182;</a>
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
            A closure is technique that allows functions to bundle variables in their local scope for access at a later time. If there was a variable x with the value of ten in the namespace for instance, even after that code executed, we could refer back to the namespace and x would still be 10. That's a little dry; fortunately the idea is easier to illustrate in code using a function with a function inside it.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In&nbsp;[1]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span></span><span class="k">def</span> <span class="nf">add_ten_to_things</span><span class="p">():</span>
    <span class="c1"># inside this function is a scope</span>
    <span class="c1"># we&#39;ll call it "outer scope"</span>
    <span class="n">x</span> <span class="o">=</span> <span class="mi">10</span>
    <span class="k">def</span> <span class="nf">inner</span><span class="p">(</span><span class="n">y</span><span class="p">):</span>
        <span class="c1"># this function has a scope</span>
        <span class="c1"># we&#39;ll call it "inner scope"</span>
        <span class="k">return</span> <span class="n">x</span> <span class="o">+</span> <span class="n">y</span>
    <span class="k">return</span> <span class="n">inner</span>
</pre>
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
            Notice how in the inner function we refer to the outer scope (to the variable x) and then return the inner scope? This is the mechanism that allows closures to work: that x is now packaged into the returned inner(). Let's see how it can be accessed:
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In&nbsp;[13]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span></span><span class="c1"># we call the original add_ten_to_things() function that returns the inner function/namespace</span>
<span class="n">add_ten</span> <span class="o">=</span> <span class="n">add_ten_to_things</span><span class="p">()</span>

<span class="c1"># we pass something for "y" and it will still be able to add 10 to it</span>
<span class="nb">print</span><span class="p">(</span><span class="n">add_ten</span><span class="p">(</span><span class="mi">20</span><span class="p">))</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_stream output_stdout output_text">
              <pre>30
</pre>
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
            Because 10 is stored in the local namespace of the outer function that produces the new function, 10 can still be accessed by it. A function that makes functions that add ten to things isn't especially useful, however:
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In&nbsp;[3]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span></span><span class="k">def</span> <span class="nf">add_x_to_things</span><span class="p">(</span><span class="n">x</span><span class="p">):</span>
    <span class="k">def</span> <span class="nf">adder</span><span class="p">(</span><span class="n">y</span><span class="p">):</span>
        <span class="k">return</span> <span class="n">x</span> <span class="o">+</span> <span class="n">y</span>
    <span class="k">return</span> <span class="n">adder</span>

<span class="n">increase_by_five</span> <span class="o">=</span> <span class="n">add_x_to_things</span><span class="p">(</span><span class="mi">5</span><span class="p">)</span>
<span class="n">increase_by_ten</span> <span class="o">=</span> <span class="n">add_x_to_things</span><span class="p">(</span><span class="mi">10</span><span class="p">)</span>

<span class="n">one_plus_five</span> <span class="o">=</span> <span class="n">increase_by_five</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
<span class="n">one_plus_ten</span> <span class="o">=</span> <span class="n">increase_by_ten</span><span class="p">(</span><span class="mi">6</span><span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="n">one_plus_five</span><span class="p">,</span> <span class="n">one_plus_ten</span><span class="p">)</span>
</pre>
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
            You'd be forgiven for wondering what the point of that would be. It makes more sense once you realize you can pass arguments to the outer function and that they will be accessible to the inner one. To illustrate, consider the following example, where a function can make several types of greeter builders depending on what is passed to the outer function.
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In&nbsp;[4]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span></span><span class="c1"># the outer function</span>
<span class="k">def</span> <span class="nf">greeter_maker</span><span class="p">(</span><span class="n">greeting</span><span class="p">):</span>
    <span class="c1"># inner function</span>
    <span class="k">def</span> <span class="nf">greeter</span><span class="p">(</span><span class="n">name</span><span class="p">):</span>
        <span class="nb">print</span><span class="p">(</span><span class="n">greeting</span> <span class="o">+</span> <span class="s2">","</span><span class="p">,</span> <span class="n">name</span><span class="p">)</span>
    <span class="c1"># outer function returns the inner </span>
    <span class="k">return</span> <span class="n">greeter</span>


<span class="n">formal_greeter</span> <span class="o">=</span> <span class="n">greeter_maker</span><span class="p">(</span><span class="s2">"Hello, pleased to meet you"</span><span class="p">)</span>
<span class="n">casual_greeter</span> <span class="o">=</span> <span class="n">greeter_maker</span><span class="p">(</span><span class="s2">"Heyo"</span><span class="p">)</span>
</pre>
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
            In action:
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In&nbsp;[5]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span></span><span class="n">formal_greeter</span><span class="p">(</span><span class="s2">"Josh"</span><span class="p">)</span>
<span class="n">formal_greeter</span><span class="p">(</span><span class="s2">"Sruthi"</span><span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_stream output_stdout output_text">
              <pre>Hello, pleased to meet you, Josh
Hello, pleased to meet you, Sruthi
</pre>
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
            Another builder:
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In&nbsp;[6]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span></span><span class="n">casual_greeter</span><span class="p">(</span><span class="s2">"Lucy"</span><span class="p">)</span>
<span class="n">casual_greeter</span><span class="p">(</span><span class="s2">"Jackson"</span><span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_stream output_stdout output_text">
              <pre>Heyo, Lucy
Heyo, Jackson
</pre>
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
            While this show some flexibility that could be made into something useful, it can be hard to see just what a powerful idea this idea is without some context, so we will look at one more example. Consider the following class:
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In&nbsp;[7]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span></span><span class="k">class</span> <span class="nc">Person</span><span class="p">(</span><span class="nb">object</span><span class="p">):</span>
    <span class="k">def</span> <span class="nf">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">name</span><span class="p">,</span> <span class="n">age</span><span class="p">):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">name</span> <span class="o">=</span> <span class="n">name</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">age</span> <span class="o">=</span> <span class="n">age</span>
</pre>
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
            This is an extremely simple Python class that models a Person with a name and age. It's probably obvious to the any hypothetical user of this class that "name" is a string and "age' is an integer (or at least a number or some kind). However, as Python is dynamically typed, there is nothing in the language itself to enforce this. Consider the following:
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In&nbsp;[8]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span></span><span class="c1"># everything goes according to plan...</span>
<span class="n">christian</span> <span class="o">=</span> <span class="n">Person</span><span class="p">(</span><span class="s2">"Christian Slater"</span><span class="p">,</span> <span class="mi">49</span><span class="p">)</span>

<span class="c1"># whoops, wrong order...</span>
<span class="n">rami</span> <span class="o">=</span> <span class="n">Person</span><span class="p">(</span><span class="mi">37</span><span class="p">,</span> <span class="s2">"Rami Malek"</span><span class="p">)</span>

<span class="c1"># gets nane </span>
<span class="nb">print</span><span class="p">(</span><span class="n">christian</span><span class="o">.</span><span class="n">name</span><span class="p">)</span>
<span class="c1"># not what we though we&#39;d get</span>
<span class="nb">print</span><span class="p">(</span><span class="n">rami</span><span class="o">.</span><span class="n">name</span><span class="p">)</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_stream output_stdout output_text">
              <pre>Christian Slater
37
</pre>
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
            This program will run just fine until sometime downstream when someone tries to do a computation a involving rami's name or age but has the wrong type of data (ie, age += 1 and finds it's a string). Consider the following usage of a closure to prevent this (this is much simpler than it seems once you see it in context so hang on):
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In&nbsp;[9]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span></span><span class="c1"># takes a dictionary of attributes-&gt;types, and a model</span>
<span class="k">def</span> <span class="nf">typechecking_builder</span><span class="p">(</span><span class="n">required_params</span><span class="p">,</span> <span class="n">model</span><span class="p">):</span>
    
    <span class="k">def</span> <span class="nf">_builder</span><span class="p">(</span><span class="n">attributes_passed</span><span class="p">):</span>
        <span class="c1"># iterate through the dict that was passed to the outer function</span>
        <span class="k">for</span> <span class="n">k</span> <span class="ow">in</span> <span class="n">attributes_passed</span><span class="o">.</span><span class="n">keys</span><span class="p">():</span>
            <span class="n">current_param</span> <span class="o">=</span> <span class="n">attributes_passed</span><span class="p">[</span><span class="n">k</span><span class="p">]</span>
            <span class="n">type_required</span> <span class="o">=</span> <span class="n">required_params</span><span class="p">[</span><span class="n">k</span><span class="p">]</span>
            <span class="c1"># ensure they&#39;re what we&#39;ve been told to expect</span>
            <span class="k">try</span><span class="p">:</span>
                <span class="k">assert</span> <span class="nb">type</span><span class="p">(</span><span class="n">current_param</span><span class="p">)</span> <span class="o">==</span> <span class="n">type_required</span>
                <span class="nb">print</span><span class="p">(</span><span class="s2">"Type check passed for"</span><span class="p">,</span> <span class="n">current_param</span><span class="p">,</span> <span class="s2">"of type"</span><span class="p">,</span> <span class="n">type_required</span><span class="p">)</span>
            <span class="c1"># raise an error if they&#39;re not</span>
            <span class="k">except</span> <span class="ne">AssertionError</span><span class="p">:</span>
                <span class="nb">print</span><span class="p">(</span><span class="s2">"</span><span class="se">\t</span><span class="s2">found"</span><span class="p">,</span> <span class="n">current_param</span><span class="p">,</span> <span class="s2">"of type"</span><span class="p">,</span> <span class="nb">type</span><span class="p">(</span><span class="n">current_param</span><span class="p">),</span> <span class="s2">"Required:"</span><span class="p">,</span> <span class="n">type_required</span><span class="p">)</span>
                <span class="k">raise</span> <span class="ne">TypeError</span><span class="p">(</span><span class="s2">"Type check failed for:"</span><span class="p">,</span> <span class="n">k</span><span class="p">)</span> <span class="c1"># whatever you want to do for exception handling</span>
    <span class="c1"># return the type checking function</span>
    <span class="k">return</span> <span class="n">_builder</span>
</pre>
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
            We can now make a builder that will type check for us, telling the function what it should expect when it is called:
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In&nbsp;[14]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span></span><span class="c1"># make people, thier name is a string, thier age is an int, they&#39;re of type Person</span>
<span class="n">person_builder</span> <span class="o">=</span> <span class="n">typechecking_builder</span><span class="p">({</span><span class="s2">"name"</span><span class="p">:</span> <span class="nb">str</span><span class="p">,</span> <span class="s2">"age"</span><span class="p">:</span><span class="nb">int</span><span class="p">},</span> <span class="n">Person</span><span class="p">)</span>
</pre>
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
            When we use this, it will check the types we passed:
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In&nbsp;[11]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span></span><span class="n">carly</span> <span class="o">=</span> <span class="n">person_builder</span><span class="p">({</span><span class="s2">"name"</span><span class="p">:</span> <span class="s2">"Carly Chaikin"</span><span class="p">,</span> <span class="s2">"age"</span><span class="p">:</span> <span class="mi">28</span><span class="p">})</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_stream output_stdout output_text">
              <pre>Type check passed for 28 of type &lt;class &#39;int&#39;&gt;
Type check passed for Carly Chaikin of type &lt;class &#39;str&#39;&gt;
</pre>
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
            Now, if we make the simple mistake from before, we get feedback right away:
          </p>
        </div>
      </div>
    </div>
    
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In&nbsp;[12]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span></span><span class="n">sunita</span> <span class="o">=</span> <span class="n">person_builder</span><span class="p">({</span><span class="s2">"name"</span><span class="p">:</span> <span class="mi">32</span><span class="p">,</span> <span class="s2">"age"</span><span class="p">:</span> <span class="s2">"Sunita Mani"</span><span class="p">})</span>
</pre>
            </div>
          </div>
        </div>
      </div>
      
      <div class="output_wrapper">
        <div class="output">
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_stream output_stdout output_text">
              <pre>	found Sunita Mani of type &lt;class &#39;str&#39;&gt; Required: &lt;class &#39;int&#39;&gt;
</pre>
            </div>
          </div>
          
          <div class="output_area">
            <div class="prompt">
            </div>
            
            <div class="output_subarea output_text output_error">
              <pre>
<span class="ansi-red-fg">---------------------------------------------------------------------------</span>
<span class="ansi-red-fg">AssertionError</span>                            Traceback (most recent call last)
<span class="ansi-green-fg">&lt;ipython-input-9-c17e99b9bc9e&gt;</span> in <span class="ansi-cyan-fg">_builder</span><span class="ansi-blue-fg">(attributes_passed)</span>
<span class="ansi-green-intense-fg ansi-bold">     10</span>             <span class="ansi-green-fg">try</span><span class="ansi-blue-fg">:</span>
<span class="ansi-green-fg">---&gt; 11</span><span class="ansi-red-fg">                 </span><span class="ansi-green-fg">assert</span> type<span class="ansi-blue-fg">(</span>current_param<span class="ansi-blue-fg">)</span> <span class="ansi-blue-fg">==</span> type_required
<span class="ansi-green-intense-fg ansi-bold">     12</span>                 print<span class="ansi-blue-fg">(</span><span class="ansi-blue-fg">&#34;Type check passed for&#34;</span><span class="ansi-blue-fg">,</span> current_param<span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">&#34;of type&#34;</span><span class="ansi-blue-fg">,</span> type_required<span class="ansi-blue-fg">)</span>

<span class="ansi-red-fg">AssertionError</span>: 

During handling of the above exception, another exception occurred:

<span class="ansi-red-fg">TypeError</span>                                 Traceback (most recent call last)
<span class="ansi-green-fg">&lt;ipython-input-12-cc51cc9b497c&gt;</span> in <span class="ansi-cyan-fg">&lt;module&gt;</span>
<span class="ansi-green-fg">----&gt; 1</span><span class="ansi-red-fg"> </span>sunita <span class="ansi-blue-fg">=</span> person_builder<span class="ansi-blue-fg">(</span><span class="ansi-blue-fg">{</span><span class="ansi-blue-fg">&#34;name&#34;</span><span class="ansi-blue-fg">:</span> <span class="ansi-cyan-fg">32</span><span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">&#34;age&#34;</span><span class="ansi-blue-fg">:</span> <span class="ansi-blue-fg">&#34;Sunita Mani&#34;</span><span class="ansi-blue-fg">}</span><span class="ansi-blue-fg">)</span>

<span class="ansi-green-fg">&lt;ipython-input-9-c17e99b9bc9e&gt;</span> in <span class="ansi-cyan-fg">_builder</span><span class="ansi-blue-fg">(attributes_passed)</span>
<span class="ansi-green-intense-fg ansi-bold">     14</span>             <span class="ansi-green-fg">except</span> AssertionError<span class="ansi-blue-fg">:</span>
<span class="ansi-green-intense-fg ansi-bold">     15</span>                 print<span class="ansi-blue-fg">(</span><span class="ansi-blue-fg">&#34;\tfound&#34;</span><span class="ansi-blue-fg">,</span> current_param<span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">&#34;of type&#34;</span><span class="ansi-blue-fg">,</span> type<span class="ansi-blue-fg">(</span>current_param<span class="ansi-blue-fg">)</span><span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">&#34;Required:&#34;</span><span class="ansi-blue-fg">,</span> type_required<span class="ansi-blue-fg">)</span>
<span class="ansi-green-fg">---&gt; 16</span><span class="ansi-red-fg">                 </span><span class="ansi-green-fg">raise</span> TypeError<span class="ansi-blue-fg">(</span><span class="ansi-blue-fg">&#34;Type check failed for:&#34;</span><span class="ansi-blue-fg">,</span> k<span class="ansi-blue-fg">)</span> <span class="ansi-red-fg"># whatever you want to do for exception handling</span>
<span class="ansi-green-intense-fg ansi-bold">     17</span>     <span class="ansi-red-fg"># return the type checking function</span>
<span class="ansi-green-intense-fg ansi-bold">     18</span>     <span class="ansi-green-fg">return</span> _builder

<span class="ansi-red-fg">TypeError</span>: (&#39;Type check failed for:&#39;, &#39;age&#39;)</pre>
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
            ...and every Person we build will be type checked!
          </p>
        </div>
      </div>
    </div>
  </div>
</div>**