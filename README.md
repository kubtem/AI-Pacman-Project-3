# AI-Pacman-Project-3
<div class="main" id="top">
    <div id="main-header" class="main-header">
  
    

<div class="search" role="search">
  <div class="search-input-wrap">
    <input type="text" id="search-input" class="search-input" tabindex="0" placeholder="Search CS 188 Fall 2024" aria-label="Search CS 188 Fall 2024" autocomplete="off">
    <label for="search-input" class="search-label"><svg viewBox="0 0 24 24" class="search-icon"><use xlink:href="#svg-search"></use></svg></label>
  </div>
  <div id="search-results" class="search-results"></div>
</div>

  
  
  
    <nav aria-label="Auxiliary" class="aux-nav">
  <ul class="aux-nav-list">
    
      <li class="aux-nav-list-item">
        <a href="#" class="site-button">
          Dark Mode
        </a>
      </li>
    
      <li class="aux-nav-list-item">
        <a href="https://edstem.org/us/courses/62175" class="site-button">
          Ed
        </a>
      </li>
    
      <li class="aux-nav-list-item">
        <a href="https://cs-188.com/" class="site-button">
          OH Queue
        </a>
      </li>
    
      <li class="aux-nav-list-item">
        <a href="https://forms.gle/P6L93Ypanex5zqjR7" class="site-button">
          Extensions Form
        </a>
      </li>
    
      <li class="aux-nav-list-item">
        <a href="https://inst.eecs.berkeley.edu/~cs188/textbook/" class="site-button">
          Textbook
        </a>
      </li>
    
      <li class="aux-nav-list-item">
        <a href="https://forms.gle/wKRiFqCQcHVpPQtu8" class="site-button">
          Feedback Form
        </a>
      </li>
    
  </ul>
</nav>

  
</div>

    <div class="main-content-wrap">
      <nav aria-label="Breadcrumb" class="breadcrumb-nav">
  <ol class="breadcrumb-nav-list">
    <li class="breadcrumb-nav-list-item"><a href="/~cs188/fa24/projects/">Projects</a></li>
    <li class="breadcrumb-nav-list-item"><span>Project 3</span></li>
  </ol>
</nav>
      <div id="main-content" class="main-content">
        <main>
          
            <h1 class="no_toc" id="project-3-reinforcement-learning">
  
  
    <a href="#project-3-reinforcement-learning" class="anchor-heading" aria-labelledby="project-3-reinforcement-learning"><svg viewBox="0 0 16 16" aria-hidden="true"><use xlink:href="#svg-link"></use></svg></a> Project 3: Reinforcement Learning
  
  
</h1>
    

<div style="text-align:center;">
Due: <b>Thursday, October 10th, 11:59 PM PT</b>.
</div><hr>
<h2 class="no_toc text-delta" id="table-of-contents">
  
  
    <a href="#table-of-contents" class="anchor-heading" aria-labelledby="table-of-contents"><svg viewBox="0 0 16 16" aria-hidden="true"><use xlink:href="#svg-link"></use></svg></a> Table of contents
  
  
</h2>
    

<ul id="markdown-toc">
  <li><a href="#introduction" id="markdown-toc-introduction">Introduction</a></li>
  <li><a href="#mdps" id="markdown-toc-mdps">MDPs</a></li>
  <li><a href="#question-1-5-points-value-iteration" id="markdown-toc-question-1-5-points-value-iteration">Question 1 (5 points): Value Iteration</a></li>
  <li><a href="#question-2-5-points-policies" id="markdown-toc-question-2-5-points-policies">Question 2 (5 points): Policies</a></li>
  <li><a href="#question-3-5-points-q-learning" id="markdown-toc-question-3-5-points-q-learning">Question 3 (5 points): Q-Learning</a></li>
  <li><a href="#question-4-2-points-epsilon-greedy" id="markdown-toc-question-4-2-points-epsilon-greedy">Question 4 (2 points): Epsilon Greedy</a></li>
  <li><a href="#question-5-1-point-q-learning-and-pacman" id="markdown-toc-question-5-1-point-q-learning-and-pacman">Question 5 (1 point): Q-Learning and Pacman</a></li>
  <li><a href="#question-6-3-points-approximate-q-learning" id="markdown-toc-question-6-3-points-approximate-q-learning">Question 6 (3 points): Approximate Q-Learning</a></li>
  <li><a href="#submission" id="markdown-toc-submission">Submission</a></li>
</ul><hr>
<h2 id="introduction">
  
  
    <a href="#introduction" class="anchor-heading" aria-labelledby="introduction"><svg viewBox="0 0 16 16" aria-hidden="true"><use xlink:href="#svg-link"></use></svg></a> Introduction
  
  
</h2>
    

<p>In this project, you will implement value iteration and Q-learning. You will test your agents first on Gridworld (from class), then apply them to a simulated robot controller (Crawler) and Pacman.</p>

<p>As in previous projects, this project includes an autograder for you to grade your solutions on your machine. This can be run on all questions with the command:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python autograder.py
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>It can be run for one particular question, such as q2, by:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python autograder.py <span class="nt">-q</span> q2
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>It can be run for one particular test by commands of the form:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python autograder.py <span class="nt">-t</span> test_cases/q2/1-bridge-grid
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>The code for this project contains the following files, available as a <a href="/~cs188/fa24/assets/projects/reinforcement.zip">zip archive</a></p>

<div class="table-wrapper"><table>
    <tbody>
      <tr>
        <td colspan="2"><b>Files you'll edit:</b></td>
      </tr>
      <tr>
        <td><code>valueIterationAgents.py</code></td>
        <td>A value iteration agent for solving known MDPs.</td>
      </tr>
      <tr>
        <td><code>qlearningAgents.py</code></td>
        <td>Q-learning agents for Gridworld, Crawler and Pacman.</td>
      </tr>
      <tr>
        <td><code>analysis.py</code></td>
        <td>A file to put your answers to questions given in the project.</td>
      </tr>
      <tr>
        <td colspan="2"><b>Files you might want to look at:</b></td>
      </tr>
      <tr>
        <td><code>mdp.py</code></td>
        <td>Defines methods on general MDPs.</td>
      </tr>
      <tr>
        <td><code>learningAgents.py</code></td>
        <td>Defines the base classes <code>ValueEstimationAgent</code> and <code>QLearningAgent</code>, which your agents will extend.</td>
      </tr>
      <tr>
        <td><code>util.py</code></td>
        <td>Utilities, including <code>util.Counter</code>, which is particularly useful for Q-learners.</td>
      </tr>
      <tr>
        <td><code>gridworld.py</code></td>
        <td>The Gridworld implementation.</td>
      </tr>
      <tr>
        <td><code>featureExtractors.py</code></td>
        <td>Classes for extracting features on (state, action) pairs. Used for the approximate Q-learning agent (in <code>qlearningAgents.py</code>).</td>
      </tr>
      <tr>
        <td colspan="2"><b>Supporting files you can ignore:</b></td>
      </tr>
      <tr>
        <td><code>environment.py</code></td>
        <td>Abstract class for general reinforcement learning environments. Used by <code>gridworld.py</code>.</td>
      </tr>
      <tr>
        <td><code>graphicsGridworldDisplay.py</code></td>
        <td>Gridworld graphical display.</td>
      </tr>
      <tr>
        <td><code>graphicsUtils.py</code></td>
        <td>Graphics utilities.</td>
      </tr>
      <tr>
        <td><code>textGridworldDisplay.py</code></td>
        <td>Plug-in for the Gridworld text interface.</td>
      </tr>
      <tr>
        <td><code>crawler.py</code></td>
        <td>The crawler code and test harness. You will run this but not edit it.</td>
      </tr>
      <tr>
        <td><code>graphicsCrawlerDisplay.py</code></td>
        <td>GUI for the crawler robot.</td>
      </tr>
      <tr>
        <td><code>autograder.py</code></td>
        <td>Project autograder</td>
      </tr>
      <tr>
        <td><code>testParser.py</code></td>
        <td>Parses autograder test and solution files</td>
      </tr>
      <tr>
        <td><code>testClasses.py</code></td>
        <td>General autograding test classes</td>
      </tr>
      <tr>
        <td><code>test_cases/</code></td>
        <td>Directory containing the test cases for each question</td>
      </tr>
      <tr>
        <td><code>reinforcementTestClasses.py</code></td>
        <td>Project 3 specific autograding test classes</td>
      </tr>
    </tbody>
</table></div>

<p><strong>Files to Edit and Submit</strong>: You will fill in portions of <code class="language-plaintext highlighter-rouge">valueIterationAgents.py</code>, <code class="language-plaintext highlighter-rouge">qlearningAgents.py</code>, and <code class="language-plaintext highlighter-rouge">analysis.py</code> during the assignment. Once you have completed the assignment, you will submit these files to Gradescope (for instance, you can upload all <code class="language-plaintext highlighter-rouge">.py</code> files in the folder). Please do not change the other files in this distribution.</p>

<p><strong>Evaluation</strong>: Your code will be autograded for technical correctness. Please do not change the names of any provided functions or classes within the code, or you will wreak havoc on the autograder. However, the correctness of your implementation – not the autograder’s judgements – will be the final judge of your score. If necessary, we will review and grade assignments individually to ensure that you receive due credit for your work.</p>

<p><strong>Academic Dishonesty</strong>: We will be checking your code against other submissions in the class for logical redundancy. If you copy someone else’s code and submit it with minor changes, we will know. These cheat detectors are quite hard to fool, so please don’t try. We trust you all to submit your own work only; please don’t let us down. If you do, we will pursue the strongest consequences available to us.</p>

<p><strong>Getting Help</strong>: You are not alone! If you find yourself stuck on something, contact the course staff for help. Office hours, section, and the discussion forum are there for your support; please use them. If you can’t make our office hours, let us know and we will schedule more. We want these projects to be rewarding and instructional, not frustrating and demoralizing. But, we don’t know when or how to help unless you ask.</p>

<p><strong>Discussion</strong>: Please be careful not to post spoilers.</p><hr>
<h2 id="mdps">
  
  
    <a href="#mdps" class="anchor-heading" aria-labelledby="mdps"><svg viewBox="0 0 16 16" aria-hidden="true"><use xlink:href="#svg-link"></use></svg></a> MDPs
  
  
</h2>
    

<p>To get started, run Gridworld in manual control mode, which uses the arrow keys:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python gridworld.py <span class="nt">-m</span>
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>You will see the two-exit layout from class. The blue dot is the agent. Note that when you press up, the agent only actually moves north 80% of the time. Such is the life of a Gridworld agent!</p>

<p>You can control many aspects of the simulation. A full list of options is available by running:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python gridworld.py <span class="nt">-h</span>
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>The default agent moves randomly</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python gridworld.py <span class="nt">-g</span> MazeGrid
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>You should see the random agent bounce around the grid until it happens upon an exit. Not the finest hour for an AI agent.</p>

<p>Note: The Gridworld MDP is such that you first must enter a pre-terminal state (the double boxes shown in the GUI) and then take the special ‘exit’ action before the episode actually ends (in the true terminal state called <code class="language-plaintext highlighter-rouge">TERMINAL_STATE</code>, which is not shown in the GUI). If you run an episode manually, your total return may be less than you expected, due to the discount rate (<code class="language-plaintext highlighter-rouge">-d</code> to change; 0.9 by default).</p>

<p>Look at the console output that accompanies the graphical output (or use <code class="language-plaintext highlighter-rouge">-t</code> for all text). You will be told about each transition the agent experiences (to turn this off, use <code class="language-plaintext highlighter-rouge">-q</code>).</p>

<p>As in Pacman, positions are represented by <code class="language-plaintext highlighter-rouge">(x, y)</code> Cartesian coordinates and any arrays are indexed by <code class="language-plaintext highlighter-rouge">[x][y]</code>, with <code class="language-plaintext highlighter-rouge">'north'</code> being the direction of increasing <code class="language-plaintext highlighter-rouge">y</code>, etc. By default, most transitions will receive a reward of zero, though you can change this with the living reward option (<code class="language-plaintext highlighter-rouge">-r</code>).</p><hr>
<h2 id="question-1-5-points-value-iteration">
  
  
    <a href="#question-1-5-points-value-iteration" class="anchor-heading" aria-labelledby="question-1-5-points-value-iteration"><svg viewBox="0 0 16 16" aria-hidden="true"><use xlink:href="#svg-link"></use></svg></a> Question 1 (5 points): Value Iteration
  
  
</h2>
    

<p>Recall the value iteration state update equation:</p>

<span><span class="katex-display"><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>V</mi><mrow><mi>k</mi><mo>+</mo><mn>1</mn></mrow></msub><mo stretchy="false">(</mo><mi>s</mi><mo stretchy="false">)</mo><mo>←</mo><munder><mrow><mi>max</mi><mo>⁡</mo></mrow><mi>a</mi></munder><munder><mo>∑</mo><msup><mi>s</mi><mo mathvariant="normal" lspace="0em" rspace="0em">′</mo></msup></munder><mi>T</mi><mo stretchy="false">(</mo><mi>s</mi><mo separator="true">,</mo><mi>a</mi><mo separator="true">,</mo><msup><mi>s</mi><mo mathvariant="normal" lspace="0em" rspace="0em">′</mo></msup><mo stretchy="false">)</mo><mrow><mo fence="true">[</mo><mi>R</mi><mo stretchy="false">(</mo><mi>s</mi><mo separator="true">,</mo><mi>a</mi><mo separator="true">,</mo><msup><mi>s</mi><mo mathvariant="normal" lspace="0em" rspace="0em">′</mo></msup><mo stretchy="false">)</mo><mo>+</mo><mi>γ</mi><msub><mi>V</mi><mi>k</mi></msub><mo stretchy="false">(</mo><msup><mi>s</mi><mo mathvariant="normal" lspace="0em" rspace="0em">′</mo></msup><mo stretchy="false">)</mo><mo fence="true">]</mo></mrow></mrow><annotation encoding="application/x-tex">V_{k+1}(s) \leftarrow \max_a \sum_{s'} T(s,a,s')\left[R(s,a,s') + \gamma V_k(s')\right]</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.2222em;">V</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3361em;"><span class="" style="top: -2.55em; margin-left: -0.2222em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mathnormal mtight" style="margin-right: 0.0315em;">k</span><span class="mbin mtight">+</span><span class="mord mtight">1</span></span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.2083em;"><span class=""></span></span></span></span></span></span><span class="mopen">(</span><span class="mord mathnormal">s</span><span class="mclose">)</span><span class="mspace" style="margin-right: 0.2778em;"></span><span class="mrel">←</span><span class="mspace" style="margin-right: 0.2778em;"></span></span><span class="base"><span class="strut" style="height: 2.344em; vertical-align: -1.294em;"></span><span class="mop op-limits"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.4306em;"><span class="" style="top: -2.4em; margin-left: 0em;"><span class="pstrut" style="height: 3em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight">a</span></span></span><span class="" style="top: -3em;"><span class="pstrut" style="height: 3em;"></span><span class=""><span class="mop">max</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.7em;"><span class=""></span></span></span></span></span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mop op-limits"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 1.05em;"><span class="" style="top: -1.856em; margin-left: 0em;"><span class="pstrut" style="height: 3.05em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mtight"><span class="mord mathnormal mtight">s</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.6828em;"><span class="" style="top: -2.786em; margin-right: 0.0714em;"><span class="pstrut" style="height: 2.5em;"></span><span class="sizing reset-size3 size1 mtight"><span class="mord mtight"><span class="mord mtight">′</span></span></span></span></span></span></span></span></span></span></span></span><span class="" style="top: -3.05em;"><span class="pstrut" style="height: 3.05em;"></span><span class=""><span class="mop op-symbol large-op">∑</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 1.294em;"><span class=""></span></span></span></span></span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord mathnormal" style="margin-right: 0.1389em;">T</span><span class="mopen">(</span><span class="mord mathnormal">s</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord mathnormal">a</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord"><span class="mord mathnormal">s</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.8019em;"><span class="" style="top: -3.113em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mtight">′</span></span></span></span></span></span></span></span></span><span class="mclose">)</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="minner"><span class="mopen delimcenter" style="top: 0em;">[</span><span class="mord mathnormal" style="margin-right: 0.0077em;">R</span><span class="mopen">(</span><span class="mord mathnormal">s</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord mathnormal">a</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord"><span class="mord mathnormal">s</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.8019em;"><span class="" style="top: -3.113em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mtight">′</span></span></span></span></span></span></span></span></span><span class="mclose">)</span><span class="mspace" style="margin-right: 0.2222em;"></span><span class="mbin">+</span><span class="mspace" style="margin-right: 0.2222em;"></span><span class="mord mathnormal" style="margin-right: 0.0556em;">γ</span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.2222em;">V</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3361em;"><span class="" style="top: -2.55em; margin-left: -0.2222em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight" style="margin-right: 0.0315em;">k</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.15em;"><span class=""></span></span></span></span></span></span><span class="mopen">(</span><span class="mord"><span class="mord mathnormal">s</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.8019em;"><span class="" style="top: -3.113em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mtight">′</span></span></span></span></span></span></span></span></span><span class="mclose">)</span><span class="mclose delimcenter" style="top: 0em;">]</span></span></span></span></span></span></span>

<p>Write a value iteration agent in <code class="language-plaintext highlighter-rouge">ValueIterationAgent</code>, which has been partially specified for you in <code class="language-plaintext highlighter-rouge">valueIterationAgents.py</code>. Your value iteration agent is an offline planner, not a reinforcement learning agent, and so the relevant training option is the number of iterations of value iteration it should run (option <code class="language-plaintext highlighter-rouge">-i</code>) in its initial planning phase. <code class="language-plaintext highlighter-rouge">ValueIterationAgent</code> takes an MDP on construction and runs value iteration for the specified number of iterations before the constructor returns.</p>

<p>Value iteration computes <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi></mrow><annotation encoding="application/x-tex">k</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.6944em;"></span><span class="mord mathnormal" style="margin-right: 0.0315em;">k</span></span></span></span></span>-step estimates of the optimal values, <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>V</mi><mi>k</mi></msub></mrow><annotation encoding="application/x-tex">V_k</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.8333em; vertical-align: -0.15em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.2222em;">V</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3361em;"><span class="" style="top: -2.55em; margin-left: -0.2222em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight" style="margin-right: 0.0315em;">k</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.15em;"><span class=""></span></span></span></span></span></span></span></span></span></span>. In addition to <code class="language-plaintext highlighter-rouge">runValueIteration</code>, implement the following methods for <code class="language-plaintext highlighter-rouge">ValueIterationAgent</code> using <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>V</mi><mi>k</mi></msub></mrow><annotation encoding="application/x-tex">V_k</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.8333em; vertical-align: -0.15em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.2222em;">V</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3361em;"><span class="" style="top: -2.55em; margin-left: -0.2222em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight" style="margin-right: 0.0315em;">k</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.15em;"><span class=""></span></span></span></span></span></span></span></span></span></span>:</p>

<ul>
  <li><code class="language-plaintext highlighter-rouge">computeActionFromValues(state)</code> computes the best action according to the value function given by self.values.</li>
  <li><code class="language-plaintext highlighter-rouge">computeQValueFromValues(state, action)</code> returns the Q-value of the (state, action) pair given by the value function given by <code class="language-plaintext highlighter-rouge">self.values</code>.</li>
</ul>

<p>These quantities are all displayed in the GUI: values are numbers in squares, Q-values are numbers in square quarters, and policies are arrows out from each square.</p>

<p>Important: Use the “batch” version of value iteration where each vector <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>V</mi><mi>k</mi></msub></mrow><annotation encoding="application/x-tex">V_k</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.8333em; vertical-align: -0.15em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.2222em;">V</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3361em;"><span class="" style="top: -2.55em; margin-left: -0.2222em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight" style="margin-right: 0.0315em;">k</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.15em;"><span class=""></span></span></span></span></span></span></span></span></span></span> is computed from a fixed vector <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>V</mi><mrow><mi>k</mi><mo>−</mo><mn>1</mn></mrow></msub></mrow><annotation encoding="application/x-tex">V_{k−1}</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.8917em; vertical-align: -0.2083em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.2222em;">V</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3361em;"><span class="" style="top: -2.55em; margin-left: -0.2222em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mathnormal mtight" style="margin-right: 0.0315em;">k</span><span class="mbin mtight">−</span><span class="mord mtight">1</span></span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.2083em;"><span class=""></span></span></span></span></span></span></span></span></span></span> (like in lecture), not the “online” version where one single weight vector is updated in place. This means that when a state’s value is updated in iteration <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi></mrow><annotation encoding="application/x-tex">k</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.6944em;"></span><span class="mord mathnormal" style="margin-right: 0.0315em;">k</span></span></span></span></span> based on the values of its successor states, the successor state values used in the value update computation should be those from iteration <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi><mo>−</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">k−1</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.7778em; vertical-align: -0.0833em;"></span><span class="mord mathnormal" style="margin-right: 0.0315em;">k</span><span class="mspace" style="margin-right: 0.2222em;"></span><span class="mbin">−</span><span class="mspace" style="margin-right: 0.2222em;"></span></span><span class="base"><span class="strut" style="height: 0.6444em;"></span><span class="mord">1</span></span></span></span></span> (even if some of the successor states had already been updated in iteration 
<span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi></mrow><annotation encoding="application/x-tex">k</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.6944em;"></span><span class="mord mathnormal" style="margin-right: 0.0315em;">k</span></span></span></span></span>). The difference is discussed in <a href="https://web.archive.org/web/20230417150626/https://web.stanford.edu/class/psych209/Readings/SuttonBartoIPRLBook2ndEd.pdf">Sutton &amp; Barto</a> in Chapter 4.1 on page 91.</p>

<p><em>Note</em>: A policy synthesized from values of depth <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi></mrow><annotation encoding="application/x-tex">k</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.6944em;"></span><span class="mord mathnormal" style="margin-right: 0.0315em;">k</span></span></span></span></span> (which reflect the next <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi></mrow><annotation encoding="application/x-tex">k</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.6944em;"></span><span class="mord mathnormal" style="margin-right: 0.0315em;">k</span></span></span></span></span> rewards) will actually reflect the next <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi><mo>+</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">k+1</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.7778em; vertical-align: -0.0833em;"></span><span class="mord mathnormal" style="margin-right: 0.0315em;">k</span><span class="mspace" style="margin-right: 0.2222em;"></span><span class="mbin">+</span><span class="mspace" style="margin-right: 0.2222em;"></span></span><span class="base"><span class="strut" style="height: 0.6444em;"></span><span class="mord">1</span></span></span></span></span> rewards (i.e. you return <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>π</mi><mrow><mi>k</mi><mo>+</mo><mn>1</mn></mrow></msub></mrow><annotation encoding="application/x-tex">\pi_{k+1}</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.6389em; vertical-align: -0.2083em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.0359em;">π</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3361em;"><span class="" style="top: -2.55em; margin-left: -0.0359em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mathnormal mtight" style="margin-right: 0.0315em;">k</span><span class="mbin mtight">+</span><span class="mord mtight">1</span></span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.2083em;"><span class=""></span></span></span></span></span></span></span></span></span></span>). Similarly, the Q-values will also reflect one more reward than the values (i.e. you return <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>Q</mi><mrow><mi>k</mi><mo>+</mo><mn>1</mn></mrow></msub></mrow><annotation encoding="application/x-tex">Q_{k+1}</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.8917em; vertical-align: -0.2083em;"></span><span class="mord"><span class="mord mathnormal">Q</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3361em;"><span class="" style="top: -2.55em; margin-left: 0em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mathnormal mtight" style="margin-right: 0.0315em;">k</span><span class="mbin mtight">+</span><span class="mord mtight">1</span></span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.2083em;"><span class=""></span></span></span></span></span></span></span></span></span></span>).</p>

<p>You should return the synthesized policy <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>π</mi><mrow><mi>k</mi><mo>+</mo><mn>1</mn></mrow></msub></mrow><annotation encoding="application/x-tex">\pi_{k+1}</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.6389em; vertical-align: -0.2083em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.0359em;">π</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3361em;"><span class="" style="top: -2.55em; margin-left: -0.0359em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mathnormal mtight" style="margin-right: 0.0315em;">k</span><span class="mbin mtight">+</span><span class="mord mtight">1</span></span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.2083em;"><span class=""></span></span></span></span></span></span></span></span></span></span>.</p>

<p><em>Hint</em>: You may optionally use the <code class="language-plaintext highlighter-rouge">util.Counter</code> class in <code class="language-plaintext highlighter-rouge">util.py</code>, which is a dictionary with a default value of zero. However, be careful with <code class="language-plaintext highlighter-rouge">argMax</code>: the actual argmax you want may be a key not in the counter!</p>

<p><em>Note</em>: Make sure to handle the case when a state has no available actions in an MDP (think about what this means for future rewards).</p>

<p>To test your implementation, run the autograder:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python autograder.py <span class="nt">-q</span> q1
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>The following command loads your <code class="language-plaintext highlighter-rouge">ValueIterationAgent</code>, which will compute a policy and execute it 10 times. Press a key to cycle through values, Q-values, and the simulation. You should find that the value of the start state (<code class="language-plaintext highlighter-rouge">V(start)</code>, which you can read off of the GUI) and the empirical resulting average reward (printed after the 10 rounds of execution finish) are quite close.</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python gridworld.py <span class="nt">-a</span> value <span class="nt">-i</span> 100 <span class="nt">-k</span> 10
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p><em>Hint</em>: On the default <code class="language-plaintext highlighter-rouge">BookGrid</code>, running value iteration for 5 iterations should give you this output:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python gridworld.py <span class="nt">-a</span> value <span class="nt">-i</span> 5
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p><img style="display:block;margin-left:auto;margin-right:auto;width:600px" alt="Value iteration diagram" src="/~cs188/fa24/assets/projects/value_iter_diagram.png"></p>

<p><em>Grading</em>: Your value iteration agent will be graded on a new grid. We will check your values, Q-values, and policies after fixed numbers of iterations and at convergence (e.g. after 100 iterations).</p><hr>
<h2 id="question-2-5-points-policies">
  
  
    <a href="#question-2-5-points-policies" class="anchor-heading" aria-labelledby="question-2-5-points-policies"><svg viewBox="0 0 16 16" aria-hidden="true"><use xlink:href="#svg-link"></use></svg></a> Question 2 (5 points): Policies
  
  
</h2>
    

<p>Consider the <code class="language-plaintext highlighter-rouge">DiscountGrid</code> layout, shown below. This grid has two terminal states with positive payoff (in the middle row), a close exit with payoff +1 and a distant exit with payoff +10. The bottom row of the grid consists of terminal states with negative payoff (shown in red); each state in this “cliff” region has payoff -10. The starting state is the yellow square. We distinguish between two types of paths: (1) paths that “risk the cliff” and travel near the bottom row of the grid; these paths are shorter but risk earning a large negative payoff, and are represented by the red arrow in the figure below. (2) paths that “avoid the cliff” and travel along the top edge of the grid. These paths are longer but are less likely to incur huge negative payoffs. These paths are represented by the green arrow in the figure below.</p>

<p><img style="display:block;margin-left:auto;margin-right:auto;width:400px" alt="Paths in gridworld" src="/~cs188/fa24/assets/projects/value_2_paths.png"></p>

<p>In this question, you will choose settings of the discount, noise, and living reward parameters for this MDP to produce optimal policies of several different types. <strong>Your setting of the parameter values for each part should have the property that, if your agent followed its optimal policy without being subject to any noise, it would exhibit the given behavior.</strong> If a particular behavior is not achieved for any setting of the parameters, assert that the policy is impossible by returning the string <code class="language-plaintext highlighter-rouge">'NOT POSSIBLE'</code>.</p>

<p>Here are the optimal policy types you should attempt to produce:</p>

<ol>
  <li>Prefer the close exit (+1), risking the cliff (-10)</li>
  <li>Prefer the close exit (+1), but avoiding the cliff (-10)</li>
  <li>Prefer the distant exit (+10), risking the cliff (-10)</li>
  <li>Prefer the distant exit (+10), avoiding the cliff (-10)</li>
  <li>Avoid both exits and the cliff (so an episode should never terminate)</li>
</ol>

<p>To see what behavior a set of numbers ends up in, run the following command to see a GUI:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python gridworld.py <span class="nt">-g</span> DiscountGrid <span class="nt">-a</span> value <span class="nt">--discount</span> <span class="o">[</span>YOUR_DISCOUNT] <span class="nt">--noise</span> <span class="o">[</span>YOUR_NOISE] <span class="nt">--livingReward</span> <span class="o">[</span>YOUR_LIVING_REWARD]
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>To check your answers, run the autograder:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python autograder.py <span class="nt">-q</span> q2
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p><code class="language-plaintext highlighter-rouge">question2a()</code> through <code class="language-plaintext highlighter-rouge">question2e()</code> should each return a 3-item tuple of <code class="language-plaintext highlighter-rouge">(discount, noise, living reward)</code> in <code class="language-plaintext highlighter-rouge">analysis.py</code>.</p>

<p><em>Note</em>: You can check your policies in the GUI. For example, using a correct answer to 3(a), the arrow in (0,1) should point east, the arrow in (1,1) should also point east, and the arrow in (2,1) should point north.</p>

<p><em>Note</em>: On some machines you may not see an arrow. In this case, press a button on the keyboard to switch to qValue display, and mentally calculate the policy by taking the arg max of the available qValues for each state.</p>

<p><em>Grading</em>: We will check that the desired policy is returned in each case.</p><hr>
<h2 id="question-3-5-points-q-learning">
  
  
    <a href="#question-3-5-points-q-learning" class="anchor-heading" aria-labelledby="question-3-5-points-q-learning"><svg viewBox="0 0 16 16" aria-hidden="true"><use xlink:href="#svg-link"></use></svg></a> Question 3 (5 points): Q-Learning
  
  
</h2>
    

<p>Note that your value iteration agent does not actually learn from experience. Rather, it ponders its MDP model to arrive at a complete policy before ever interacting with a real environment. When it does interact with the environment, it simply follows the precomputed policy (e.g. it becomes a reflex agent). This distinction may be subtle in a simulated environment like a Gridword, but it’s very important in the real world, where the real MDP is not available.</p>

<p>You will now write a Q-learning agent, which does very little on construction, but instead learns by trial and error from interactions with the environment through its <code class="language-plaintext highlighter-rouge">update(state, action, nextState, reward)</code> method. A stub of a Q-learner is specified in <code class="language-plaintext highlighter-rouge">QLearningAgent</code> in <code class="language-plaintext highlighter-rouge">qlearningAgents.py</code>, and you can select it with the option <code class="language-plaintext highlighter-rouge">'-a q'</code>. For this question, you must implement the <code class="language-plaintext highlighter-rouge">update</code>, <code class="language-plaintext highlighter-rouge">computeValueFromQValues</code>, <code class="language-plaintext highlighter-rouge">getQValue</code>, and <code class="language-plaintext highlighter-rouge">computeActionFromQValues</code> methods.</p>

<p><em>Note</em>: For <code class="language-plaintext highlighter-rouge">computeActionFromQValues</code>, you should break ties randomly for better behavior. The <code class="language-plaintext highlighter-rouge">random.choice()</code> function will help. In a particular state, actions that your agent hasn’t seen before still have a Q-value, specifically a Q-value of zero, and if all of the actions that your agent has seen before have a negative Q-value, an unseen action may be optimal.</p>

<p><em>Important</em>: Make sure that in your <code class="language-plaintext highlighter-rouge">computeValueFromQValues</code> and <code class="language-plaintext highlighter-rouge">computeActionFromQValues</code> functions, you only access Q values by calling <code class="language-plaintext highlighter-rouge">getQValue</code>. This abstraction will be useful for question 10 when you override <code class="language-plaintext highlighter-rouge">getQValue</code> to use features of state-action pairs rather than state-action pairs directly.</p>

<p>With the Q-learning update in place, you can watch your Q-learner learn under manual control, using the keyboard:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python gridworld.py <span class="nt">-a</span> q <span class="nt">-k</span> 5 <span class="nt">-m</span>
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>Recall that <code class="language-plaintext highlighter-rouge">-k</code> will control the number of episodes your agent gets to learn. Watch how the agent learns about the state it was just in, not the one it moves to, and “leaves learning in its wake.” Hint: to help with debugging, you can turn off noise by using the <code class="language-plaintext highlighter-rouge">--noise 0.0</code> parameter (though this obviously makes Q-learning less interesting). If you manually steer Pacman north and then east along the optimal path for four episodes, you should see the following Q-values:</p>

<p><img style="display:block;margin-left:auto;margin-right:auto;width:600px" alt="Q-value diagram" src="/~cs188/fa24/assets/projects/q_learning.png"></p>

<p><em>Grading</em>: We will run your Q-learning agent and check that it learns the same Q-values and policy as our reference implementation when each is presented with the same set of examples. To grade your implementation, run the autograder:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python autograder.py <span class="nt">-q</span> q3
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div><hr>
<h2 id="question-4-2-points-epsilon-greedy">
  
  
    <a href="#question-4-2-points-epsilon-greedy" class="anchor-heading" aria-labelledby="question-4-2-points-epsilon-greedy"><svg viewBox="0 0 16 16" aria-hidden="true"><use xlink:href="#svg-link"></use></svg></a> Question 4 (2 points): Epsilon Greedy
  
  
</h2>
    

<p>Complete your Q-learning agent by implementing epsilon-greedy action selection in <code class="language-plaintext highlighter-rouge">getAction</code>, meaning it chooses random actions an epsilon fraction of the time, and follows its current best Q-values otherwise. Note that choosing a random action may result in choosing the best action - that is, you should not choose a random sub-optimal action, but rather any random legal action.</p>

<p>You can choose an element from a list uniformly at random by calling the <code class="language-plaintext highlighter-rouge">random.choice</code> function. You can simulate a binary variable with probability <code class="language-plaintext highlighter-rouge">p</code> of success by using <code class="language-plaintext highlighter-rouge">util.flipCoin(p)</code>, which returns <code class="language-plaintext highlighter-rouge">True</code> with probability <code class="language-plaintext highlighter-rouge">p</code> and <code class="language-plaintext highlighter-rouge">False</code> with probability <code class="language-plaintext highlighter-rouge">1-p</code>.</p>

<p>After implementing the <code class="language-plaintext highlighter-rouge">getAction</code> method, observe the following behavior of the agent in <code class="language-plaintext highlighter-rouge">GridWorld</code> (with epsilon = 0.3).</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python gridworld.py <span class="nt">-a</span> q <span class="nt">-k</span> 100
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>Your final Q-values should resemble those of your value iteration agent, especially along well-traveled paths. However, your average returns will be lower than the Q-values predict because of the random actions and the initial learning phase.</p>

<p>You can also observe the following simulations for different epsilon values. Does that behavior of the agent match what you expect?</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python gridworld.py <span class="nt">-a</span> q <span class="nt">-k</span> 100 <span class="nt">--noise</span> 0.0 <span class="nt">-e</span> 0.1
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python gridworld.py <span class="nt">-a</span> q <span class="nt">-k</span> 100 <span class="nt">--noise</span> 0.0 <span class="nt">-e</span> 0.9
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>To test your implementation, run the autograder:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python autograder.py <span class="nt">-q</span> q4
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>With no additional code, you should now be able to run a Q-learning crawler robot:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python crawler.py
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>If this doesn’t work, you’ve probably written some code too specific to the <code class="language-plaintext highlighter-rouge">GridWorld</code> problem and you should make it more general to all MDPs.</p>

<p>This will invoke the crawling robot from class using your Q-learner. Play around with the various learning parameters to see how they affect the agent’s policies and actions. Note that the step delay is a parameter of the simulation, whereas the learning rate and epsilon are parameters of your learning algorithm, and the discount factor is a property of the environment.</p><hr>
<h2 id="question-5-1-point-q-learning-and-pacman">
  
  
    <a href="#question-5-1-point-q-learning-and-pacman" class="anchor-heading" aria-labelledby="question-5-1-point-q-learning-and-pacman"><svg viewBox="0 0 16 16" aria-hidden="true"><use xlink:href="#svg-link"></use></svg></a> Question 5 (1 point): Q-Learning and Pacman
  
  
</h2>
    

<p>Time to play some Pacman! Pacman will play games in two phases. In the first phase, <em>training</em>, Pacman will begin to learn about the values of positions and actions. Because it takes a very long time to learn accurate Q-values even for tiny grids, Pacman’s training games run in quiet mode by default, with no GUI (or console) display. Once Pacman’s training is complete, he will enter <em>testing</em> mode. When testing, Pacman’s <code class="language-plaintext highlighter-rouge">self.epsilon</code> and <code class="language-plaintext highlighter-rouge">self.alpha</code> will be set to 0.0, effectively stopping Q-learning and disabling exploration, in order to allow Pacman to exploit his learned policy. Test games are shown in the GUI by default. Without any code changes you should be able to run Q-learning Pacman for very tiny grids as follows:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python pacman.py <span class="nt">-p</span> PacmanQAgent <span class="nt">-x</span> 2000 <span class="nt">-n</span> 2010 <span class="nt">-l</span> smallGrid
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>Note that <code class="language-plaintext highlighter-rouge">PacmanQAgent</code> is already defined for you in terms of the <code class="language-plaintext highlighter-rouge">QLearningAgent</code> you’ve already written. <code class="language-plaintext highlighter-rouge">PacmanQAgent</code> is only different in that it has default learning parameters that are more effective for the Pacman problem (<code class="language-plaintext highlighter-rouge">epsilon=0.05, alpha=0.2, gamma=0.8</code>). You will receive full credit for this question if the command above works without exceptions and your agent wins at least 80% of the time. The autograder will run 100 test games after the 2000 training games.</p>

<p><em>Hint</em>: If your <code class="language-plaintext highlighter-rouge">QLearningAgent</code> works for <code class="language-plaintext highlighter-rouge">gridworld.py</code> and <code class="language-plaintext highlighter-rouge">crawler.py</code> but does not seem to be learning a good policy for Pacman on <code class="language-plaintext highlighter-rouge">smallGrid</code>, it may be because your <code class="language-plaintext highlighter-rouge">getAction</code> and/or <code class="language-plaintext highlighter-rouge">computeActionFromQValues</code> methods do not in some cases properly consider unseen actions. In particular, because unseen actions have by definition a Q-value of zero, if all of the actions that have been seen have negative Q-values, an unseen action may be optimal. Beware of the <code class="language-plaintext highlighter-rouge">argMax</code> function from <code class="language-plaintext highlighter-rouge">util.Counter</code>!</p>

<p>To grade your answer, run:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python autograder.py <span class="nt">-q</span> q5
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p><em>Note</em>: If you want to experiment with learning parameters, you can use the option <code class="language-plaintext highlighter-rouge">-a</code>, for example <code class="language-plaintext highlighter-rouge">-a epsilon=0.1,alpha=0.3,gamma=0.7</code>. These values will then be accessible as <code class="language-plaintext highlighter-rouge">self.epsilon</code>, <code class="language-plaintext highlighter-rouge">self.gamma</code> and <code class="language-plaintext highlighter-rouge">self.alpha</code> inside the agent.</p>

<p><em>Note</em>: While a total of 2010 games will be played, the first 2000 games will not be displayed because of the option <code class="language-plaintext highlighter-rouge">-x 2000</code>, which designates the first 2000 games for training (no output). Thus, you will only see Pacman play the last 10 of these games. The number of training games is also passed to your agent as the option <code class="language-plaintext highlighter-rouge">numTraining</code>.</p>

<p><em>Note</em>: If you want to watch 10 training games to see what’s going on, use the command:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python pacman.py <span class="nt">-p</span> PacmanQAgent <span class="nt">-n</span> 10 <span class="nt">-l</span> smallGrid <span class="nt">-a</span> <span class="nv">numTraining</span><span class="o">=</span>10
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>During training, you will see output every 100 games with statistics about how Pacman is faring. Epsilon is positive during training, so Pacman will play poorly even after having learned a good policy: this is because he occasionally makes a random exploratory move into a ghost. As a benchmark, it should take between 1000 and 1400 games before Pacman’s rewards for a 100 episode segment becomes positive, reflecting that he’s started winning more than losing. By the end of training, it should remain positive and be fairly high (between 100 and 350).</p>

<p>Make sure you understand what is happening here: the MDP state is the exact board configuration facing Pacman, with the now complex transitions describing an entire ply of change to that state. The intermediate game configurations in which Pacman has moved but the ghosts have not replied are not MDP states, but are bundled in to the transitions.</p>

<p>Once Pacman is done training, he should win very reliably in test games (at least 90% of the time), since now he is exploiting his learned policy.</p>

<p>However, you will find that training the same agent on the seemingly simple <code class="language-plaintext highlighter-rouge">mediumGrid</code> does not work well. In our implementation, Pacman’s average training rewards remain negative throughout training. At test time, he plays badly, probably losing all of his test games. Training will also take a long time, despite its ineffectiveness.</p>

<p>Pacman fails to win on larger layouts because each board configuration is a separate state with separate Q-values. He has no way to generalize that running into a ghost is bad for all positions. Obviously, this approach will not scale.</p><hr>
<h2 id="question-6-3-points-approximate-q-learning">
  
  
    <a href="#question-6-3-points-approximate-q-learning" class="anchor-heading" aria-labelledby="question-6-3-points-approximate-q-learning"><svg viewBox="0 0 16 16" aria-hidden="true"><use xlink:href="#svg-link"></use></svg></a> Question 6 (3 points): Approximate Q-Learning
  
  
</h2>
    

<p>Implement an approximate Q-learning agent that learns weights for features of states, where many states might share the same features. Write your implementation in <code class="language-plaintext highlighter-rouge">ApproximateQAgent</code> class in <code class="language-plaintext highlighter-rouge">qlearningAgents.py</code>, which is a subclass of <code class="language-plaintext highlighter-rouge">PacmanQAgent</code>.</p>

<p><em>Note</em>: Approximate Q-learning assumes the existence of a feature function <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>f</mi><mo stretchy="false">(</mo><mi>s</mi><mo separator="true">,</mo><mi>a</mi><mo stretchy="false">)</mo></mrow><annotation encoding="application/x-tex">f(s,a)</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord mathnormal" style="margin-right: 0.1076em;">f</span><span class="mopen">(</span><span class="mord mathnormal">s</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord mathnormal">a</span><span class="mclose">)</span></span></span></span></span> over state and action pairs, which yields a vector <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mo stretchy="false">[</mo><msub><mi>f</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>s</mi><mo separator="true">,</mo><mi>a</mi><mo stretchy="false">)</mo><mo separator="true">,</mo><mo>…</mo><mo separator="true">,</mo><msub><mi>f</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>s</mi><mo separator="true">,</mo><mi>a</mi><mo stretchy="false">)</mo><mo separator="true">,</mo><mo>…</mo><mo separator="true">,</mo><msub><mi>f</mi><mi>n</mi></msub><mo stretchy="false">(</mo><mi>s</mi><mo separator="true">,</mo><mi>a</mi><mo stretchy="false">)</mo><mo stretchy="false">]</mo></mrow><annotation encoding="application/x-tex">[f_1(s,a), \dots, f_i(s,a), \dots, f_n(s,a)]</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mopen">[</span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.1076em;">f</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3011em;"><span class="" style="top: -2.55em; margin-left: -0.1076em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight">1</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.15em;"><span class=""></span></span></span></span></span></span><span class="mopen">(</span><span class="mord mathnormal">s</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord mathnormal">a</span><span class="mclose">)</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="minner">…</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.1076em;">f</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3117em;"><span class="" style="top: -2.55em; margin-left: -0.1076em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight">i</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.15em;"><span class=""></span></span></span></span></span></span><span class="mopen">(</span><span class="mord mathnormal">s</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord mathnormal">a</span><span class="mclose">)</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="minner">…</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.1076em;">f</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.1514em;"><span class="" style="top: -2.55em; margin-left: -0.1076em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight">n</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.15em;"><span class=""></span></span></span></span></span></span><span class="mopen">(</span><span class="mord mathnormal">s</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord mathnormal">a</span><span class="mclose">)]</span></span></span></span></span> of feature values. We provide feature functions for you in <code class="language-plaintext highlighter-rouge">featureExtractors.py</code>. Feature vectors are <code class="language-plaintext highlighter-rouge">util.Counter</code> (like a dictionary) objects containing the non-zero pairs of features and values; all omitted features have value zero. So, instead of an vector where the index in the vector defines which feature is which, we have the keys in the dictionary define the idenity of the feature.</p>

<p>The approximate Q-function takes the following form:</p>

<span><span class="katex-display"><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mi>Q</mi><mo stretchy="false">(</mo><mi>s</mi><mo separator="true">,</mo><mi>a</mi><mo stretchy="false">)</mo><mo>=</mo><munderover><mo>∑</mo><mrow><mi>i</mi><mo>=</mo><mn>1</mn></mrow><mi>n</mi></munderover><msub><mi>f</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>s</mi><mo separator="true">,</mo><mi>a</mi><mo stretchy="false">)</mo><msub><mi>w</mi><mi>i</mi></msub></mrow><annotation encoding="application/x-tex">Q(s,a)=\sum_{i=1}^n f_i(s,a) w_i</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord mathnormal">Q</span><span class="mopen">(</span><span class="mord mathnormal">s</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord mathnormal">a</span><span class="mclose">)</span><span class="mspace" style="margin-right: 0.2778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.2778em;"></span></span><span class="base"><span class="strut" style="height: 2.9291em; vertical-align: -1.2777em;"></span><span class="mop op-limits"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 1.6514em;"><span class="" style="top: -1.8723em; margin-left: 0em;"><span class="pstrut" style="height: 3.05em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mathnormal mtight">i</span><span class="mrel mtight">=</span><span class="mord mtight">1</span></span></span></span><span class="" style="top: -3.05em;"><span class="pstrut" style="height: 3.05em;"></span><span class=""><span class="mop op-symbol large-op">∑</span></span></span><span class="" style="top: -4.3em; margin-left: 0em;"><span class="pstrut" style="height: 3.05em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight">n</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 1.2777em;"><span class=""></span></span></span></span></span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.1076em;">f</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3117em;"><span class="" style="top: -2.55em; margin-left: -0.1076em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight">i</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.15em;"><span class=""></span></span></span></span></span></span><span class="mopen">(</span><span class="mord mathnormal">s</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord mathnormal">a</span><span class="mclose">)</span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.0269em;">w</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3117em;"><span class="" style="top: -2.55em; margin-left: -0.0269em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight">i</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.15em;"><span class=""></span></span></span></span></span></span></span></span></span></span></span>

<p>where each weight <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>w</mi><mi>i</mi></msub></mrow><annotation encoding="application/x-tex">w_i</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.5806em; vertical-align: -0.15em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.0269em;">w</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3117em;"><span class="" style="top: -2.55em; margin-left: -0.0269em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight">i</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.15em;"><span class=""></span></span></span></span></span></span></span></span></span></span> is associated with a particular feature <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>f</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>s</mi><mo separator="true">,</mo><mi>a</mi><mo stretchy="false">)</mo></mrow><annotation encoding="application/x-tex">f_i(s,a)</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.1076em;">f</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3117em;"><span class="" style="top: -2.55em; margin-left: -0.1076em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight">i</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.15em;"><span class=""></span></span></span></span></span></span><span class="mopen">(</span><span class="mord mathnormal">s</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord mathnormal">a</span><span class="mclose">)</span></span></span></span></span>. In your code, you should implement the weight vector as a dictionary mapping features (which the feature extractors will return) to weight values. You will update your weight vectors similarly to how you updated Q-values:</p>

<span><span class="katex-display"><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>w</mi><mi>i</mi></msub><mo>←</mo><msub><mi>w</mi><mi>i</mi></msub><mo>+</mo><mi>α</mi><mo>⋅</mo><mtext>difference</mtext><mo>⋅</mo><msub><mi>f</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>s</mi><mo separator="true">,</mo><mi>a</mi><mo stretchy="false">)</mo></mrow><annotation encoding="application/x-tex">w_i \leftarrow w_i + \alpha \cdot \text{difference} \cdot f_i(s,a)</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.5806em; vertical-align: -0.15em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.0269em;">w</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3117em;"><span class="" style="top: -2.55em; margin-left: -0.0269em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight">i</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.15em;"><span class=""></span></span></span></span></span></span><span class="mspace" style="margin-right: 0.2778em;"></span><span class="mrel">←</span><span class="mspace" style="margin-right: 0.2778em;"></span></span><span class="base"><span class="strut" style="height: 0.7333em; vertical-align: -0.15em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.0269em;">w</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3117em;"><span class="" style="top: -2.55em; margin-left: -0.0269em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight">i</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.15em;"><span class=""></span></span></span></span></span></span><span class="mspace" style="margin-right: 0.2222em;"></span><span class="mbin">+</span><span class="mspace" style="margin-right: 0.2222em;"></span></span><span class="base"><span class="strut" style="height: 0.4445em;"></span><span class="mord mathnormal" style="margin-right: 0.0037em;">α</span><span class="mspace" style="margin-right: 0.2222em;"></span><span class="mbin">⋅</span><span class="mspace" style="margin-right: 0.2222em;"></span></span><span class="base"><span class="strut" style="height: 0.6944em;"></span><span class="mord text"><span class="mord">difference</span></span><span class="mspace" style="margin-right: 0.2222em;"></span><span class="mbin">⋅</span><span class="mspace" style="margin-right: 0.2222em;"></span></span><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord"><span class="mord mathnormal" style="margin-right: 0.1076em;">f</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.3117em;"><span class="" style="top: -2.55em; margin-left: -0.1076em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathnormal mtight">i</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.15em;"><span class=""></span></span></span></span></span></span><span class="mopen">(</span><span class="mord mathnormal">s</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord mathnormal">a</span><span class="mclose">)</span></span></span></span></span></span>

<span><span class="katex-display"><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mtext>difference</mtext><mo>=</mo><mrow><mo fence="true">(</mo><mi>r</mi><mo>+</mo><mi>γ</mi><munder><mrow><mi>max</mi><mo>⁡</mo></mrow><msup><mi>a</mi><mo mathvariant="normal" lspace="0em" rspace="0em">′</mo></msup></munder><mi>Q</mi><mo stretchy="false">(</mo><msup><mi>s</mi><mo mathvariant="normal" lspace="0em" rspace="0em">′</mo></msup><mo separator="true">,</mo><msup><mi>a</mi><mo mathvariant="normal" lspace="0em" rspace="0em">′</mo></msup><mo stretchy="false">)</mo><mo fence="true">)</mo></mrow><mo>−</mo><mi>Q</mi><mo stretchy="false">(</mo><mi>s</mi><mo separator="true">,</mo><mi>a</mi><mo stretchy="false">)</mo></mrow><annotation encoding="application/x-tex">\text{difference} = \left( r + \gamma \max_{a'}Q(s',a') \right) - Q(s,a)</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.6944em;"></span><span class="mord text"><span class="mord">difference</span></span><span class="mspace" style="margin-right: 0.2778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.2778em;"></span></span><span class="base"><span class="strut" style="height: 1.894em; vertical-align: -0.744em;"></span><span class="minner"><span class="mopen delimcenter" style="top: 0em;"><span class="delimsizing size2">(</span></span><span class="mord mathnormal" style="margin-right: 0.0278em;">r</span><span class="mspace" style="margin-right: 0.2222em;"></span><span class="mbin">+</span><span class="mspace" style="margin-right: 0.2222em;"></span><span class="mord mathnormal" style="margin-right: 0.0556em;">γ</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mop op-limits"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 0.4306em;"><span class="" style="top: -2.356em; margin-left: 0em;"><span class="pstrut" style="height: 3em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mtight"><span class="mord mathnormal mtight">a</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.6828em;"><span class="" style="top: -2.786em; margin-right: 0.0714em;"><span class="pstrut" style="height: 2.5em;"></span><span class="sizing reset-size3 size1 mtight"><span class="mord mtight"><span class="mord mtight">′</span></span></span></span></span></span></span></span></span></span></span></span><span class="" style="top: -3em;"><span class="pstrut" style="height: 3em;"></span><span class=""><span class="mop">max</span></span></span></span><span class="vlist-s">&ZeroWidthSpace;</span></span><span class="vlist-r"><span class="vlist" style="height: 0.744em;"><span class=""></span></span></span></span></span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord mathnormal">Q</span><span class="mopen">(</span><span class="mord"><span class="mord mathnormal">s</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.8019em;"><span class="" style="top: -3.113em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mtight">′</span></span></span></span></span></span></span></span></span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord"><span class="mord mathnormal">a</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.8019em;"><span class="" style="top: -3.113em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mtight">′</span></span></span></span></span></span></span></span></span><span class="mclose">)</span><span class="mclose delimcenter" style="top: 0em;"><span class="delimsizing size2">)</span></span></span><span class="mspace" style="margin-right: 0.2222em;"></span><span class="mbin">−</span><span class="mspace" style="margin-right: 0.2222em;"></span></span><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord mathnormal">Q</span><span class="mopen">(</span><span class="mord mathnormal">s</span><span class="mpunct">,</span><span class="mspace" style="margin-right: 0.1667em;"></span><span class="mord mathnormal">a</span><span class="mclose">)</span></span></span></span></span></span>

<p>Note that the <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mtext>difference</mtext></mrow><annotation encoding="application/x-tex">\text{difference}</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.6944em;"></span><span class="mord text"><span class="mord">difference</span></span></span></span></span></span> term is the same as in normal Q-learning, and <span><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>r</mi></mrow><annotation encoding="application/x-tex">r</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.4306em;"></span><span class="mord mathnormal" style="margin-right: 0.0278em;">r</span></span></span></span></span> is the experienced reward.</p>

<p>By default, <code class="language-plaintext highlighter-rouge">ApproximateQAgent</code> uses the <code class="language-plaintext highlighter-rouge">IdentityExtractor</code>, which assigns a single feature to every <code class="language-plaintext highlighter-rouge">(state,action)</code> pair. With this feature extractor, your approximate Q-learning agent should work identically to <code class="language-plaintext highlighter-rouge">PacmanQAgent</code>. You can test this with the following command:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python pacman.py <span class="nt">-p</span> ApproximateQAgent <span class="nt">-x</span> 2000 <span class="nt">-n</span> 2010 <span class="nt">-l</span> smallGrid
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p><em>Important</em>: <code class="language-plaintext highlighter-rouge">ApproximateQAgent</code> is a subclass of <code class="language-plaintext highlighter-rouge">QLearningAgent</code>, and it therefore shares several methods like <code class="language-plaintext highlighter-rouge">getAction</code>. Make sure that your methods in <code class="language-plaintext highlighter-rouge">QLearningAgent</code> call <code class="language-plaintext highlighter-rouge">getQValue</code> instead of accessing Q-values directly, so that when you override <code class="language-plaintext highlighter-rouge">getQValue</code> in your approximate agent, the new approximate q-values are used to compute actions.</p>

<p>Once you’re confident that your approximate learner works correctly with the identity features, run your approximate Q-learning agent with our custom feature extractor, which can learn to win with ease:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python pacman.py <span class="nt">-p</span> ApproximateQAgent <span class="nt">-a</span> <span class="nv">extractor</span><span class="o">=</span>SimpleExtractor <span class="nt">-x</span> 50 <span class="nt">-n</span> 60 <span class="nt">-l</span> mediumGrid
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>Even much larger layouts should be no problem for your <code class="language-plaintext highlighter-rouge">ApproximateQAgent</code> (<em>warning</em>: this may take a few minutes to train):</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python pacman.py <span class="nt">-p</span> ApproximateQAgent <span class="nt">-a</span> <span class="nv">extractor</span><span class="o">=</span>SimpleExtractor <span class="nt">-x</span> 50 <span class="nt">-n</span> 60 <span class="nt">-l</span> mediumClassic
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div>

<p>If you have no errors, your approximate Q-learning agent should win almost every time with these simple features, even with only 50 training games.</p>

<p><em>Grading</em>: We will run your approximate Q-learning agent and check that it learns the same Q-values and feature weights as our reference implementation when each is presented with the same set of examples. To grade your implementation, run the autograder:</p>

<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>python autograder.py <span class="nt">-q</span> q6
</code></pre></div><button type="button" aria-label="Copy code to clipboard"><svg viewBox="0 0 24 24" class="copy-icon"><use xlink:href="#svg-copy"></use></svg></button></div><hr>
<h2 id="submission">
  
  
    <a href="#submission" class="anchor-heading" aria-labelledby="submission"><svg viewBox="0 0 16 16" aria-hidden="true"><use xlink:href="#svg-link"></use></svg></a> Submission
  
  
</h2>
    

<p>In order to submit your project upload the Python files you edited. For instance, use Gradescope’s upload on all <code class="language-plaintext highlighter-rouge">.py</code> files in the project folder.</p>

          

          
        </main>
        

  <hr>
  <footer>
    

    <script>
(function() {
  var navList = document.querySelector('.aux-nav-list');
  if (!navList || !navList.firstElementChild) return;
  var darkToggle = navList.firstElementChild;
  darkToggle.addEventListener('click', (e) => {
    e.preventDefault();
    toggleDark();
  });
})();
</script>

<script src="/~cs188/fa24/assets/js/jquery.min.js"></script>
<!--
June 2024 - looks like the copy button got merged, bless
https://just-the-docs.com/docs/ui-components/code/#copy-button

<script src="/~cs188/fa24/assets/js/clipboard.min.js"></script>
<script>
// adapted from https://stackoverflow.com/a/48078807/1217368
// Waiting for https://github.com/just-the-docs/just-the-docs/pull/945
$(document).ready(function () {
  $('pre.highlight').each(function (i) {
    // create an id for the current code section
    var currentId = 'codeBlock' + i

    // find the code section and add the id to it
    var codeSection = $(this).find('code')
    codeSection.attr('id', currentId)

    // now create the button, setting the clipboard target to the id
    var btn = document.createElement('a')
    btn.setAttribute('type', 'btn')
    btn.setAttribute('class', 'badge badge-light btn-copy-code')
    btn.setAttribute('data-clipboard-target', '#' + currentId)
    btn.innerHTML = '<i class="fal fa-copy"></i> Copy'
    $(this).after(btn)
  })

  new ClipboardJS('.btn-copy-code')
})
</script>
-->

<script src="/~cs188/fa24/assets/js/tocbot.min.js"></script>
<script>
// Tries to mirror the HTML TOC
tocbot.init({
  tocSelector: '.js-toc',
  contentSelector: '.main-content',
  headingSelector: 'h2, h3',
  ignoreSelector: '.no_toc',
  hasInnerContainers: true,
  linkClass: 'nav-list-link',
  activeLinkClass: 'active',
  listClass: 'nav-list',
  listItemClass: 'nav-list-item',
  activeListItemClass: 'active',
  collapseDepth: 3,
  scrollSmooth: false,
});
</script>


    
  </footer>


      </div>
    </div>
    
      

<div class="search-overlay"></div>

    
  </div>
