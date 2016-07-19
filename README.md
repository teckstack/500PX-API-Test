## 500PX-API-Test
----
Simple code to _fetch and display data_ using [500PX API](https://github.com/500px/api-documentation). If you are a photographer this trick may save little money that you spend on hosting.<br><br>
Because you upload your photos on 500px.com site, in your profile, and access to display the same on your personal portfolio site.
<br>

But the main purpose is to save time in uploadoading the same photographs on multiple sites.
<br>

**Full Article**: <br>
http://teckstack.com/create-portfolio-with-500px-apis
<br>

**View Demo**: <br>
http://teckstack.github.io/500PX-API-Test/
<br><br>

**Steps**:
<ol>
<li>Goto https://500px.com</li>
<li>If you already have an account, please login or else create one for the access</li>
<li>Now go to "Settings" link from Profile dropdown: <br>https://500px.com/settings</li>
<li>Under settings, click on "Applications" and here you have to register your app: <br>https://500px.com/settings/applications</li>
<li>Make sure to configure all URLs correctly</li>
<li>Now you will see "JavaScript SDK Key". Copy that key and replace that in below Script. DO NOT SHARE!</li>
</ol>
<br><br>

#### HTML
<pre><code>&lt;section id="main-content" class="col-md-9"&gt;
	&lt;h2&gt;A Demo&lt;/h2&gt;
    &lt;div id="grid"&gt;&lt;/div&gt;
&lt;/section&gt;
</code></pre>
<br><br>

Include [500px.js](http://kutec.github.io/500PX-API-Test/js/500px.js) file before below script.
We are going to fetch data from [Deval Jayswal](http://500px.com/DevJayswal).
<br><br>

#### Script
<pre><code>&lt;script src="js/500px.js"&gt;&lt;/script&gt;
&lt;script src="http://ajax.googleapis.com/ajax/libs/jquery/1.8.1/jquery.min.js"&gt;&lt;/script&gt;

&lt;script&gt;
  $(function() {
      _500px.init({
          sdk_key: '1234567890123456789012345678901234567890'	//replace with your 500px js sdk key
      });

      // Get my user id
      _500px.api('/users', function(response) {
          var me = "DevJayswal";
          var siteurl = "http://500px.com/photo/"

          // Get my favorites
          _500px.api('/photos', {
              feature: 'user',
              username: me,
              total_items: 5000
          }, function(response) {
              if (response.data.photos.length == 0) {
                  alert('Nothing found! Please refresh...');
              } else {
                  $.each(response.data.photos, function() {
                      $('#grid').append('&lt;article class="post col-md-3 col-sm-4 col-xs-12 panel panel-default"&gt;&lt;h3&gt;' + this.name + '&lt;/h3&gt;&lt;a href="' + siteurl + this.id + '" target="_blank"&gt;&lt;img src="' + this.image_url + '"&gt;&lt;/a&gt;&lt;/article&gt;');
                  });
              }
          });
      });
  });
&lt;/script&gt;
</code></pre>
