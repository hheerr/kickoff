---
layout: demo
body-class: show-grid
navgroup: demo
navactive: elements
title: Elements <small>all of them in one place</small>
---
<h2>Embedded content</h2>

<h3>img</h3>
<img src="http://placekitten.com/100/100" alt="">
<a href="#"><img src="http://placekitten.com/100/100" alt=""></a>

<h3>svg</h3>

<svg style="width:200px; height:200px;">
	<circle cx="100" cy="100" r="80" fill="#00ff88"/>
	<circle cx="100" cy="100" r="50" fill="#ff0088"/>
	<circle cx="100" cy="100" r="25" fill="#fff"/>
</svg>


<h3>Pre</h3>

<pre>Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et me.</pre>

<h3>Pre > Code</h3>
<pre><code>&lt;html>
&lt;head>
&lt;/head>
&lt;body>
&lt;div class="main">

&lt;div>
&lt;/body>
&lt;/html></code></pre>

<h3>figure</h3>

<figure>
	<img src="http://placekitten.com/400/200" alt="">
	<figcaption>Figcaption content</figcaption>
</figure>

<h2>Tabular data</h2>

<table summary="Jimi Hendrix albums" class="table table-bordered table-striped">
	<caption>
		Jimi Hendrix - albums
	</caption>
	<thead>
	<tr>
		<th>Album</th>
		<th>Year</th>
		<th>Price</th>
	</tr>
	</thead>
	<tbody>
	<tr>
		<td>Are You Experienced</td>
		<td>1967</td>
		<td>$10.00</td>
	</tr>
	<tr>
		<td>Axis: Bold as Love</td>
		<td>1967</td>
		<td>$12.00</td>
	</tr>
	<tr>
		<td>Electric Ladyland</td>
		<td>1968</td>
		<td>$10.00</td>
	</tr>
	<tr>
		<td>Band of Gypsys</td>
		<td>1970</td>
		<td>$12.00</td>
	</tr>
	</tbody>
</table>

<h2>Forms</h2>

<form class="well form-horizontal">
	<fieldset>
	<legend>Inputs as descendents of labels (form legend)</legend>
	<ul class="form_items">
		<li><label>Text input </label><input type="text" value="value"></li>
		<li><label>Text input (required)</label> <input type="text" required></li>
		<li><label>Text input (with pattern requirement and placeholder)</label> <input type="text" pattern="\d{5}(-\d{4})?" title="a US Zip code, with or without the +4 exension" placeholder="12345-6789"></li>
		<li><label>Email input</label> <input type="email"></li>
		<li><label>Search input</label> <input type="search"></li>
		<li><label>Tel input</label> <input type="tel"></li>
		<li><label>URL input</label> <input type="url" placeholder="http://"></li>
		<li><label>Password input</label> <input type="password" value="password"></li>
		<li><label>Radio input</label> <input type="radio" name="rad"></li>
		<li><label>File input</label> <input type="file"></li>
		<li><label>Checkbox input</label> <input type="checkbox"></li>
		<li><label>Select field</label> <select><option>Option 01</option><option>Option 02</option></select></li>
		<li><label>Textarea</label> <textarea cols="30" rows="5" class="span6">Textarea text</textarea></li>
	</ul>
	</fieldset>

	<fieldset>
	<legend>Inputs as siblings of labels</legend>
	<ul class="form_items">
		<li><label for="ic">Color input</label> <input type="color" id="ic"></li>
		<li><label for="in">Number input</label> <input type="number" id="in" min="0" max="10"></li>
		<li><label for="ir">Range input</label> <input type="range" id="ir"></li>
		<li><label for="idd">Date input</label> <input type="date" id="idd"></li>
		<li><label for="idm">Month input</label> <input type="month" id="idm"></li>
		<li><label for="idw">Week input</label> <input type="week" id="idw"></li>
		<li><label for="idt">Datetime input</label> <input type="datetime" id="idt"></li>
		<li><label for="idtl">Datetime-local input</label> <input type="datetime-local" id="idtl"></li>
		<li><label for="irb">Radio input</label> <input type="radio" id="irb" name="rad"></li>
		<li><label for="icb">Checkbox input</label> <input type="checkbox" id="icb"></li>
		<li><input type="radio" id="irb2" name="rad"> <label for="irb2">Radio input</label></li>
		<li><input type="checkbox" id="icb2"> <label for="icb2">Checkbox input</label></li>
		<li><label for="s">Select field</label> <select id="s"><option>Option 01</option><option>Option 02</option></select></li>
		<li><label for="t">Textarea</label> <textarea id="t" cols="30" rows="5" >Textarea text</textarea></li>
	</ul>
	</fieldset>

	<fieldset>
	<legend>Clickable inputs and buttons</legend>
	<ul class="form_items">
		<li><input type="image" src="http://placekitten.com/120/124" alt="Image (input)"></li>
		<li><input class="btn" type="reset" value="Reset (input)"></li>
		<li><input class="btn" type="button" value="Button (input)"></li>
		<li><input class="btn" type="submit" value="Submit (input)"></li>
		<li><button class="btn" type="reset">Reset (button)</button></li>
		<li><button class="btn" type="button">Button (button)</button></li>
		<li><button class="btn" type="submit">Submit (button)</button></li>
	</ul>
	</fieldset>

	<fieldset id="boxsize">
	<legend>box-sizing tests</legend>
		<ul class="form_items">
			<li><input type="text" value="text"></li>
			<li><input type="email" value="email@example.com"></li>
			<li><input type="search" value="search"></li>
			<li><input type="url" value="http://"></li>
			<li><input type="password" value="password"></li>
			<li><input type="color"></li>
			<li><input type="number"></li>
			<li><input type="range"></li>
			<li><input type="date"></li>
			<li><input type="month"></li>
			<li><input type="week"></li>
			<li><input type="datetime"></li>
			<li><input type="datetime-local"></li>
			<li><input type="radio"></li>
			<li><input type="checkbox"></li>
			<li><select><option>Option 01</option><option>Option 02</option></select></li>
			<li><textarea cols="30" rows="5" >Textarea text</textarea></li>
			<li><input type="image" src="http://placehold.it/120x120" alt="Image (input)"></li>
			<li><input class="btn" type="reset" value="Reset (input)"></li>
			<li><input class="btn" type="button" value="Button (input)"></li>
			<li><input class="btn" type="submit" value="Submit (input)"></li>
			<li><button class="btn" type="reset">Reset (button)</button></li>
			<li><button class="btn" type="button">Button (button)</button></li>
			<li><button class="btn" type="submit">Submit (button)</button></li>
		</ul>
	</fieldset>
</form>