# ProgrammingWidgetLayout

<pre style="color:#000020;background:#f6f8ff;"><span style="color:#200080; font-weight:bold; ">int</span> <span style="color:#400000; ">main</span><span style="color:#308080; ">(</span><span style="color:#200080; font-weight:bold; ">int</span> argc<span style="color:#308080; ">,</span> <span style="color:#200080; font-weight:bold; ">char</span><span style="color:#308080; ">*</span> argv<span style="color:#308080; ">[</span><span style="color:#308080; ">]</span><span style="color:#308080; ">)</span>
<span style="color:#406080; ">{</span>
  <span style="color:#003060; ">QApplication</span> app<span style="color:#308080; ">(</span>argc<span style="color:#308080; ">,</span> argv<span style="color:#308080; ">)</span><span style="color:#406080; ">;</span>

  <span style="color:#003060; ">QWidget</span><span style="color:#308080; ">*</span> window <span style="color:#308080; ">=</span> <span style="color:#200080; font-weight:bold; ">new</span> <span style="color:#003060; ">QWidget</span><span style="color:#308080; ">(</span><span style="color:#308080; ">)</span><span style="color:#406080; ">;</span>
  window<span style="color:#308080; ">-</span><span style="color:#308080; ">&gt;</span>setWindowTitle<span style="color:#308080; ">(</span><span style="color:#800000; ">"</span><span style="color:#1060b6; ">QHBoxLayout Test</span><span style="color:#800000; ">"</span><span style="color:#308080; ">)</span><span style="color:#406080; ">;</span>

  window<span style="color:#308080; ">-</span><span style="color:#308080; ">&gt;</span>show<span style="color:#308080; ">(</span><span style="color:#308080; ">)</span><span style="color:#406080; ">;</span>

  <span style="color:#200080; font-weight:bold; ">return</span> app<span style="color:#308080; ">.</span>exec<span style="color:#308080; ">(</span><span style="color:#308080; ">)</span><span style="color:#406080; ">;</span>
<span style="color:#406080; ">}</span>
<span style="color:#ffffff; background:#dd9999; font-weight:bold; font-style:italic; ">}</span><span style="color:#406080; ">;</span>
</pre>
