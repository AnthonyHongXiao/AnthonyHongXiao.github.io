+++
title = "Some Markdown Grammer Issues"
date = "2024-04-14T16:07:36-05:00"
tags = ["logistics"]
+++

❌: \left\{ \right\}
<br>✅: \set{ }

❌: \\
<br>✅: \newline

❌: ^*
<br>✅: ^{\*}

❌: -
<br>✅: \_

❌: \|
<br>✅: \Vert
<br>(Note that one need to add a blackspace after \Vert when globally changing all of \| because otherwise for example \|a\| will be changed to \|Verta\vert, which is invalid.)

❌: \epsilon
<br>✅: \varepsilon