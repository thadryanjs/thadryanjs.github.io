---
id: 695
title: Some light-hearted OOP (or, Some Circumstantial Evidence That I am Still Alive)
date: 2018-05-10T11:49:39-04:00
author: admin
layout: revision
guid: http://pythoninthewyld.com/2018/05/10/689-revision-v1/
permalink: /2018/05/10/689-revision-v1/
---
&nbsp;

Hello there!

I am writing to let you know that I have cleared the summit of a couple of beastly projects and will be back to working on the site at at the usual semi-regular pace soon. I am also working on some pieces that are a little larger and more detailed than usual, but the delays should (hopefully) be offset with quality.

In the meantime, enjoy some easy-going code humor that doesn't want to hurt no one as evidence I am still around.

**<div tabindex="-1" id="notebook" class="border-box-sizing">
  <div class="container" id="notebook-container">
    <div class="cell border-box-sizing code_cell rendered">
      <div class="input">
        <div class="prompt input_prompt">
          In&nbsp;[2]:
        </div>
        
        <div class="inner_cell">
          <div class="input_area">
            <div class=" highlight hl-ipython3">
              <pre><span></span><span class="c1">### "trait" classes ###</span>
<span class="k">class</span> <span class="nc">Picker</span><span class="p">(</span><span class="nb">object</span><span class="p">):</span>
    
    <span class="k">def</span> <span class="nf">pick</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">"I&#39;m a picker..."</span><span class="p">)</span>
    
<span class="k">class</span> <span class="nc">Grinner</span><span class="p">(</span><span class="nb">object</span><span class="p">):</span>
    
    <span class="k">def</span> <span class="nf">grin</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">"I&#39;m a grinner..."</span><span class="p">)</span>
    
<span class="k">class</span> <span class="nc">Lover</span><span class="p">(</span><span class="nb">object</span><span class="p">):</span>
    
    <span class="k">def</span> <span class="nf">love</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">"I&#39;m a lover..."</span><span class="p">)</span>
    
<span class="k">class</span> <span class="nc">Sinner</span><span class="p">(</span><span class="nb">object</span><span class="p">):</span>
    
    <span class="k">def</span> <span class="nf">sin</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">"I&#39;m a sinner."</span><span class="p">)</span>
    
<span class="k">class</span> <span class="nc">Joker</span><span class="p">(</span><span class="nb">object</span><span class="p">):</span>
    
    <span class="k">def</span> <span class="nf">joke</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">"I&#39;m a joker..."</span><span class="p">)</span>
    
<span class="k">class</span> <span class="nc">Smoker</span><span class="p">(</span><span class="nb">object</span><span class="p">):</span>
    
    <span class="k">def</span> <span class="nf">smoke</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">"I&#39;m a smoker..."</span><span class="p">)</span>
        
<span class="k">class</span> <span class="nc">MidnightToker</span><span class="p">(</span><span class="nb">object</span><span class="p">):</span>
    
    <span class="k">def</span> <span class="nf">midnight_toke</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">"I&#39;m a midnight toker."</span><span class="p">)</span>
        
        
        
        
        
<span class="c1">### composed class ### </span>
<span class="k">class</span> <span class="nc">SteveMillerObj</span><span class="p">(</span><span class="n">Picker</span><span class="p">,</span> <span class="n">Grinner</span><span class="p">,</span> <span class="n">Lover</span><span class="p">,</span> 
                     <span class="n">Sinner</span><span class="p">,</span> <span class="n">Joker</span><span class="p">,</span> <span class="n">Smoker</span><span class="p">,</span> <span class="n">MidnightToker</span><span class="p">):</span>
    
    <span class="k">def</span> <span class="nf">thoughts_on_hurting_someone</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">"I don&#39;t want to hurt no one."</span><span class="p">)</span>
        
    <span class="k">def</span> <span class="nf">how_loving_is_obtained</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">"I get my loving on the run."</span><span class="p">)</span>

        
        
        
        
<span class="c1">### usage ##</span>
<span class="n">Steve_Miller</span> <span class="o">=</span> <span class="n">SteveMillerObj</span><span class="p">()</span>

<span class="c1"># use traits</span>
<span class="n">Steve_Miller</span><span class="o">.</span><span class="n">pick</span><span class="p">()</span>
<span class="n">Steve_Miller</span><span class="o">.</span><span class="n">grin</span><span class="p">()</span>
<span class="n">Steve_Miller</span><span class="o">.</span><span class="n">love</span><span class="p">()</span>
<span class="n">Steve_Miller</span><span class="o">.</span><span class="n">sin</span><span class="p">()</span>

<span class="c1"># explains ethos part 1</span>
<span class="n">Steve_Miller</span><span class="o">.</span><span class="n">thoughts_on_hurting_someone</span><span class="p">()</span>

<span class="c1"># use traits </span>
<span class="n">Steve_Miller</span><span class="o">.</span><span class="n">joke</span><span class="p">()</span>
<span class="n">Steve_Miller</span><span class="o">.</span><span class="n">smoke</span><span class="p">()</span>
<span class="n">Steve_Miller</span><span class="o">.</span><span class="n">midnight_toke</span><span class="p">()</span>

<span class="c1"># explain ethos part 2</span>
<span class="n">Steve_Miller</span><span class="o">.</span><span class="n">how_loving_is_obtained</span><span class="p">()</span>
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
              <pre>I&#39;m a picker...
I&#39;m a grinner...
I&#39;m a lover...
I&#39;m a sinner.
I don&#39;t want to hurt no one.
I&#39;m a joker...
I&#39;m a smoker...
I&#39;m a midnight toker.
I get my loving on the run.
</pre>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>**