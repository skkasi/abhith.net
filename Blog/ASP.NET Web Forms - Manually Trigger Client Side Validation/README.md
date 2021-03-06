# [ASP.NET Web Forms - Manually Trigger Client Side Validation](https://www.abhith.net/post/aspnet-web-forms-manually-trigger-client-side-validation/)
## Post Attributes
### Tags
Web-Forms SharePoint 
### Categories
ASP.NET 
### Excerpt
You can manually trigger client-side validation for ASP.NET Web Forms Server side controls. One way of doing it explained here.
### Published Date
2018-01-15 23:32:28
## Content
### Markdown
Lets say you have a web form with one more serverside controls like one below,

<pre style="font-family:Fantasque Sans Mono;font-size:13;color:gainsboro;background:#1e1e1e;"><span style="color:gray;">&lt;</span><span style="color:lightblue;">asp</span><span style="color:#b4b4b4;">:</span><span style="color:lightblue;">TextBox</span>&nbsp;<span style="color:violet;">ID</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;</span><span style="color:violet;">txtEmail</span><span style="color:#c8c8c8;">&quot;</span>&nbsp;<span style="color:burlywood;">runat</span><span style="color:burlywood;">=</span><span style="color:burlywood;">&quot;server&quot;</span>&nbsp;<span style="color:#9cdcfe;">class</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;txtBoxLarge&nbsp;textSmall&quot;</span>&nbsp;<span style="color:#9cdcfe;">placeholder</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;Enter&nbsp;Email&nbsp;Address&quot;</span><span style="color:gray;">&gt;&lt;/</span><span style="color:lightblue;">asp</span><span style="color:#b4b4b4;">:</span><span style="color:lightblue;">TextBox</span><span style="color:gray;">&gt;</span>
 
<span style="color:gray;">&lt;</span><span style="color:lightblue;">asp</span><span style="color:#b4b4b4;">:</span><span style="color:lightblue;">RequiredFieldValidator</span>&nbsp;<span style="color:violet;">ID</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;</span><span style="color:violet;">rfvEmail</span><span style="color:#c8c8c8;">&quot;</span>&nbsp;<span style="color:burlywood;">runat</span><span style="color:burlywood;">=</span><span style="color:burlywood;">&quot;server&quot;</span>&nbsp;<span style="color:violet;">ErrorMessage</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;Enter&nbsp;Email&quot;</span>&nbsp;<span style="color:violet;">Display</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;</span><span style="font-weight:bold;color:violet;">None</span><span style="color:#c8c8c8;">&quot;</span>&nbsp;<span style="color:violet;">ControlToValidate</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;</span><span style="color:violet;">txtEmail</span><span style="color:#c8c8c8;">&quot;</span>&nbsp;<span style="color:violet;">ValidationGroup</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;groupName&quot;</span><span style="color:gray;">&gt;&lt;/</span><span style="color:lightblue;">asp</span><span style="color:#b4b4b4;">:</span><span style="color:lightblue;">RequiredFieldValidator</span><span style="color:gray;">&gt;</span></pre>

And you need to do some client side operations along with client side validation, the button triggering the whole operation will be like,
<pre style="font-family:Fantasque Sans Mono;font-size:13;color:gainsboro;background:#1e1e1e;"><span style="color:gray;">&lt;</span><span style="color:lightblue;">asp</span><span style="color:#b4b4b4;">:</span><span style="color:lightblue;">Button</span>&nbsp;<span style="color:violet;">ID</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;</span><span style="color:violet;">btnSubmit</span><span style="color:#c8c8c8;">&quot;</span>&nbsp;<span style="color:violet;">CssClass</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;blueBtnLarge&quot;</span>&nbsp;<span style="color:burlywood;">runat</span><span style="color:burlywood;">=</span><span style="color:burlywood;">&quot;server&quot;</span>&nbsp;<span style="color:violet;">Text</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;Continue&quot;</span>&nbsp;<span style="color:violet;">ValidationGroup</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;groupName&quot;</span>&nbsp;<span style="color:plum;">OnClick</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;</span><span style="color:cyan;">btnSubmit_Click</span><span style="color:#c8c8c8;">&quot;</span>&nbsp;<span style="color:violet;">OnClientClick</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;</span><span style="color:cyan;">ClientSideClick</span><span style="color:#c8c8c8;">(this)&quot;</span>&nbsp;<span style="color:violet;">UseSubmitBehavior</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;False&quot;</span>&nbsp;<span style="color:gray;">/&gt;</span>
</pre>
Here **OnClick** will send request to server side and **OnClientClick** will execute on client side before control passed to server.  **OnClick** only will be triggered if **OnClientClick** returned **true**.

And the client side JavaScript function we call on **OnClientClick** will be like below,

<pre style="font-family:Fantasque Sans Mono;font-size:13;color:gainsboro;background:#1e1e1e;"><span style="color:gray;">&lt;</span><span style="color:#569cd6;">script</span>&nbsp;<span style="color:#9cdcfe;">type</span><span style="color:#b4b4b4;">=</span><span style="color:#c8c8c8;">&quot;text/javascript&quot;</span><span style="color:gray;">&gt;</span>
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">function</span>&nbsp;<span style="color:cyan;">ClientSideClick</span>(myButton)&nbsp;{
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#57a64a;">//&nbsp;Any&nbsp;operation&nbsp;before&nbsp;validation&nbsp;goes&nbsp;here
</span>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#57a64a;">//&nbsp;Client&nbsp;side&nbsp;validation
</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">if</span>&nbsp;(<span style="color:#569cd6;">typeof</span>&nbsp;(<span style="color:cyan;">window</span>.<span style="color:lightgray;">Page_ClientValidate</span>)&nbsp;<span style="color:#b4b4b4;">==</span>&nbsp;<span style="color:#d69d85;">&#39;function&#39;</span>)&nbsp;{
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">if</span>&nbsp;(<span style="color:cyan;">window</span>.<span style="color:lightgray;">Page_ClientValidate</span>(<span style="color:#d69d85;">&#39;groupName&#39;</span>)&nbsp;<span style="color:#b4b4b4;">===</span>&nbsp;<span style="color:#569cd6;">false</span>)&nbsp;{
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:violet;">document</span>.<span style="color:cyan;">getElementById</span>(<span style="color:#d69d85;">&#39;someDivElementWithErrorExplanation&#39;</span>).<span style="color:cyan;">style</span>.<span style="color:violet;">display</span>&nbsp;<span style="color:#b4b4b4;">=</span>&nbsp;<span style="color:#d69d85;">&#39;</span><span style="color:lightskyblue;">block</span><span style="color:#d69d85;">&#39;</span>;&nbsp;<span style="color:#57a64a;">//&nbsp;Showing&nbsp;error&nbsp;on&nbsp;validation,&nbsp;modify&nbsp;to&nbsp;your&nbsp;needs
</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">return</span>&nbsp;<span style="color:#569cd6;">false</span>;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:violet;">document</span>.<span style="color:cyan;">getElementById</span>(<span style="color:#d69d85;">&#39;someDivElementWithErrorExplanation&#39;</span>).<span style="color:cyan;">style</span>.<span style="color:violet;">display</span>&nbsp;<span style="color:#b4b4b4;">=</span>&nbsp;<span style="color:#d69d85;">&#39;</span><span style="color:lightskyblue;">none</span><span style="color:#d69d85;">&#39;</span>;
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#57a64a;">//&nbsp;Any&nbsp;operation&nbsp;after&nbsp;client&nbsp;side&nbsp;validation&nbsp;passess&nbsp;goes&nbsp;here.
</span>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">return</span>&nbsp;<span style="color:#569cd6;">true</span>;
&nbsp;&nbsp;&nbsp;&nbsp;}
<span style="color:gray;">&lt;/</span><span style="color:#569cd6;">script</span><span style="color:gray;">&gt;</span></pre>

That's it. Also, don't forget to notice the usage of the **ValidationGroup** all over the code above.
## Image
### Post Image
![Post Image](glenn-carstens-peters-190592.jpg) 
### Post Header Image
![Post Header Image](j-kelly-brito-256889.jpg)

## Meta Tags
### Social Description
You can manually trigger client-side validation for ASP.NET Web Forms Server side controls. One way of doing it explained here.
