mobiledetect
============

Mobiledetect is a Smarty plugin for CMS Made Simple System using Mobile_Detect PHP Class written by Serban Ghita.
For more information about Mobile_Detect class you can visit <a href="http://mobiledetect.net">mobiledetect.net</a> and 
if you feel there is some detection missing, find a bug or would like to contribute to Mobile_Detect project, you can find 
it on <a href="https://github.com/serbanghita/Mobile-Detect">Github</a>.
Description from Mobile_Detect project:
> "Mobile_Detect is a lightweight PHP class for detecting mobile devices (including tablets). It uses the User-Agent string combined with specific HTTP headers to detect the mobile environment."

### How do i use it?

After downloading function.mobiledetect.php file, you should upload it to you CMSMS folder inside "plugins" folder. 
After file was uploaded you can simply use it in your Page Template or Page by calling <code>{mobiledetect}</code> Smarty tag.
Once <code>{mobiledetect}</code> tag has been placed in your Template or Page, various $device Smarty Object attributes will become available.
With help of these Object attributes you can easily build a Template logic based on detected device.

#### Code Example

```php
{mobiledetect}
{if $device->isMobile}
	<div class="mobile-class">
		<p>We have found a Mobile device</p>
	{if $device->isTablet}
		<div class="only-tablet">
			<p>This is a Tablet device</p>
		</div>
	{elseif $device->isPhone}
		<div class="only-phone">
			<p>This is Phone device and not Tablet</p>
		</div>
	{/if}
	</div>
{/if}
```

### What parameters does it take?

You can also use include or exclude parameters listed below. Don't use both at the same time.
<ul>
	<li>(optional) include - A comma-separated list of mobile devices the data is intended for.</li>
	<li>(optional) exclude - A comma-separated list of mobile devices the data is not intended for. (Example exclude='tablet, asus')</li>
	<li>(optional) assign - Assign to a variable.</li>
</ul>

mobileswitcher
============

Mobiledetect plugin has also <code>{mobileswitcher}</code> smarty plugin included.

### What does this do?

Mobileswitcher plugin will return a link or URL based on Device detection from Mobile_Detect php class, link is only shown if detected device is truly mobile device.
Once link was clicked a session is created and $device Smarty Object attributes will be reset.
For exmaple if visitor visits your website with a mobile device and in your template you would be using
a Object attribute {$device->isMobile} which in case of a mobile device would return true,
after clicking on switcher link {$device->isMobile} would be reset to false.

### How do I use it?

Just insert the tag into your template/page like:
<code>{mobileswitcher}</code>

With assign parameter you can assign output of this plugin to a Smarty variable, which can be usefull if you want to apply some special layout around switching link
but it does not apply to a desktop device, offcourse you could also simply use {$device->isMobile}, but there are many way ways to skin the cat and there is also
a {$linktext} Smarty variable available which can be usefull if you are using "hrefonly" parameter but still want to be able to control output of link text.

#### Code Example

```php
{mobileswitcher assign='switcher' hrefonly='1' desktoptext='Go to desktop layout' mobiletext='Go to mobile layout'}
{if $switcher}
	<div class="switcher-wrapper">
		<div class="some-nice-style">
			<a class="my-switcher-link" href="{$switcher}">{$linktext}</a>
		</div>
	</div>
{/if}
```

### What parameters does it take?

<ul>
	<li>(optional) hrefonly - Will return only URL instead of link. (Example hrefonly='1')</li>
	<li>(optional) class - Class that should be applied to link.</li>
	<li>(optional) title - Value for link title attribute.</li>
	<li>(optional) tabindex - Value for link tabindex attribute.</li>
	<li>(optional) accesskey - Value for link accesskey attribute.</li>
	<li>(optional) desktoptext - Link text that should be displayed for mobile devices. Example: desktoptext='Switch to desktop version'. (Default: Desktop version)</li>
	<li>(optional) mobiletext - Link text that should be displayed for desktop. Example: mobiletext='Switch to mobile version'. (Default: Mobile version)</li>
	<li>(optional) assign - Assign this tag to a Smarty variable.</li>
</ul>
