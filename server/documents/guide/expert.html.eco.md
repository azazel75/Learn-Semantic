  ---
layout      : 'default'
css         : 'guide'

title       : 'Expert Guide'
description : 'Using Semantic UI in a production environment'
type        : 'Getting Started'
---
<%- @partial('header') %>

<div class="main container">

  <h2 class='ui header'>
    Getting Semantic UI
  </h2>

  <p>For links to download Semantic UI, check our our <a href="/guide/download.html">download page</a>.</p>

  <h2 class='ui header'>
    Setting Up
  </h2>

  <h3 class="ui header">Dependencies</h3>
  <p>Semantic uses command-line tools to build your project while theming. After getting Semantic, you will need to install <a href="http://nodejs.org/download/" target="_blank">nodejs</a> and <a href="https://github.com/gulpjs/gulp/" target="_blank">gulp</a> to run the build process.</p>

  <p>Once you're up and running. Navigate to the semantic directory and install the npm dependencies</p>
  <div class="bash code">
    # install dependencies
    npm install
    # start install script
    gulp
  </div>

  <h3 class="ui header">Installing Semantic</h3>

  <p>The first time you run gulp you will be greeted with an interactive installer</p>
  <div class="bash code">
    # install
    gulp
  </div>

  <img class="ui image" src="https://camo.githubusercontent.com/b9662e806f832c1ed8cb4c4d0e259fbcae20c222/68747470733a2f2f646c2e64726f70626f7875736572636f6e74656e742e636f6d2f752f323635373030372f696e7374616c6c2e676966">

  <p>The installer will let you select which components to include, and specify paths for your project.<p>

  <table class="ui definition table">
    <thead>
      <th></th>
      <th>Installation Type</th>
    </thead>
    <tbody>
    <tr>
      <td>Automatic</td>
      <td>Installation will use the default paths, outputing css files to <code>dist/</code> and packaging all components together</td>
    </tr>
    <tr>
      <td>Express</td>
      <td>Will let you move your site folder and your dist folder and select from a list of components to include in your concatenated release.</td>
    </tr>
    <tr>
      <td>Custom</td>
      <td>Will prompt you for all available options</td>
    </tr>
    </tbody>
  </table>

  <p>The install process will create two files: <code>semantic.json</code> stores paths for your build  and sits on the top-level of your project, <code>theme.config</code> is a <b>LESS</b> file that exists in <b>src/</b> and allows you to centrally set the themes for each UI component.</p>

  <p>The installer will also create a special folder which contains your site-specific themes. The default location for this is <code>src/site</code>. For more information on using site themes, see the theming guide below.</p>

  <h3 class="ui header">Manual Install</h3>
  <p>If you prefer these files and folders can be moved manually instead of using the installer.</p>
  <div class="bash code">
    mv semantic.json.example semantic.json
    mv src/theme.config.example src/theme.config
    mv src/_site src/site
    vi semantic.json
  </div>

  <h3>Upgrading Semantic</h3>

  <p>You can use normal package manager functions to update your project, just be sure to re-install semantic after upgrading. Re-install will <b>extend your <code>semantic.json</code> but not overwrite it</b></p>
  <div class="bash code">
    bower update
    cd ./bower_modules/semantic-ui
    gulp install
  </div>

  <div class="ui info message">For a full list of settings for <b>semantic.json</b>, check the <a href="https://github.com/Semantic-Org/Semantic-UI/blob/1.0/tasks/defaults.js">defaults values</a> which it inherits from.</div>

  <h2 class="ui header">Using Semantic Build Tools</h2>

  <h3 class="ui header">Gulp commands</h3>
  <p>After setting up your project you have access to several commands for building your css and javascript.</p>

  <div class="bash code">
    gulp # runs default task (watch)
    gulp watch # watches files for changes
    gulp build # builds all files from source
    gulp install # re-runs install
  </div>

  <p>
    Semantic creates minified, and uncompressed files in your source for both individual components, and the components specified for your packaged version.
  </p>

  <p>Keep in mind semantic will automatically adjust urls in css and add vendor-prefixes as part of the build process. This means <b>definitions and theme files do not need vendor prefixes</b>.</p>

  <div class="ui info message">
    <h4 class="ui header">Advanced Usage</h4>
    <p>In addition to the paths set in <code>semantic.json</code>, you can serve files to a second location, for example, a docs instance by using a separate config file <code>tasks/admin/docs.json</code>. Using a copy of the SUI documentation may work well internally for creating a style guide to hack on the theme designs for your project.</p>
    <div class="bash code">
      gulp serve-docs
      gulp build-docs
    </div>
  </div>

  <h3 class="ui header">Workflow</h3>

  <p>Building and watching Semantic is only necessary while adjusting your UI. This is usually the first part of building a new project, and a separate process than building-out pages in your site.</p>
  <p>During this architecting phase you can try <a href="#creating-packaged-themes">downloading different themes</a>, adjusting your <a href="#global-inheritance">site-wide settings</a> (font-family, colors, etc) and tweaking components in your site's <a href="#css-overrides">component overrides</a>.</p>
  <p>Files in the <code>examples/</code> folder of your project can be useful for testing out changes in your UI. For example, you might run <code>gulp watch</code> download a new theme to <code>src/site/themes/</code> then adjust your <code>theme.config</code> file with the name of the new theme and refresh <code>examples/kitchensink.html</code> to inspect changes in the theme.</p>
  <p>You will only need to use Semantic's build tools while refining your UI, while designing pages you can rely on the packages in <code>dist/</code> and your software stack's normal build set-up.</p>

  <p><code>gulp watch</code> will automatically recompile only the necessary definition files when you update <code>semantic.config</code> or any <code>.variables</code> or <code>.overrides</code> file.<p>

  <h2 class="ui header">Theming Concepts</h2>
  <p>
    Semantic uses an inheritance system similar to <a href="https://www.sublimetext.com/docs/2/settings.html" target="_blank">Sublime Text</a> designed to facilitate an ecosystem of theming.
  </p>
  <div class="ui three fluid steps">
    <div class="step">
      <i class="lock icon"></i>
      <div class="content">
        <div class="title">Semantic</div>
        <div class="description">Library Defaults</div>
      </div>
    </div>
    <div class="step">
      <i class="download icon"></i>
      <div class="content">
        <div class="title">Theme</div>
        <div class="description">Downloadable Packages</div>
      </div>
    </div>
    <div class="step">
      <i class="user icon"></i>
      <div class="content">
        <div class="title">Site</div>
        <div class="description">User's Overrides</div>
      </div>
    </div>
  </div>

  <p>
    Semantic definitions are written using <b>LESS</b>. Source files in Semantic cannot be imported into other <b>LESS</b> files. They must be compiled individually to preserve correct variable inheritance.
  </p>
  <p>Don't use <b>LESS</b> in your dev environment? Don't worry, Definitions only uses only pure CSS in combination with well established pre-processor features like <b>css variables</b>, <b>color adjustment functions</b>, <b>value calculations</b> and <b>@import</b> statements.</p>
  <div class="ui info message">
    <p>A SCSS port is underway for those who are persnickety about which indicating character precedes their variable declarations.</p>
    <p>Semantic only uses a minimal feature-set of our CSS preprocessor to make the library easy to port to future preprocessors.</p>
  </div>
  <h3 class="ui header">Elements of a Theme</h3>
  <p>
    Themes are composed of two separate files: a <code>.variable</code> file, which has values that modify variables for a component, and an <code>.overrides</code> file, which includes LESS rules which will be included after the default css of a definition.
  </p>
  <div class="ui message">
    In the following examples, paths all refer to default project paths, these might be adjusted in your project's <b>semantic.json</b> file.
  </div>
  <h3 class="ui header">Global Inheritance</h3>
  <p>Each component in Semantic, inherits from <code>site.variables</code>. This file contains many important site-wide defaults like <b>brand colors</b>, <b>default colors</b>, <b>size defaults</b>, <b>font-face</b>. Keeping site wide defaults central allow you to quickly adjust constraints for all components.</p>
  <p>
    <code>site.variables</code> is a "global definition" file with the same packaged theme and site theme inheritance as other definitions.
  </p>

  <h3 class="ui header">Component Inheritance</h3>
  <p>Each component in Semantic, begins its inheritance with default values from <code>site.variables</code>, and then defines its own variables as part of a default theme. The default theme then can be modified by a packaged theme, or by a site theme.</p>
  <p>For example, <code>ui button</code> loads variables in the following inheritance order:</p>
  <div class="ui large ordered relaxed divided list">
    <div class="item">
      <div class="content">
        <div class="header">Site variables</div>
        <div class="list">
          <div class="item">
            Defaults pulled from <code>src/themes/default/site.variables</code>
          </div>
          <div class="item">
            Theme overrides pulled for site from <code>src/themes/{themename}/site.variables</code>
          </div>
          <div class="item">
            Site overrides pulled from <code>src/site/site.variables</code>
          </div>
        </div>
      </div>
    </div>
    <div class="item">
      <div class="content">
        <div class="header">Button variables</div>
        <div class="list">
          <div class="item">
            Button default variables from <code>src/themes/default/elements/button.variables</code>
          </div>
          <div class="item">
            Button theme variables from <code>src/themes/{themename}/elements/button.variables</code>
          </div>
          <div class="item">
            Site's button theme variables from <code>src/site/elements/button.variables</code>
          </div>
        </div>
      </div>
    </div>
  </div>
  <h3 class="ui header">CSS Overrides</h3>

  <p>If additional CSS, not included in the definition, is necessary for a theme, or to adjust an element for your site, it is recommended to use an <code>.override</code> file.</p>

  <p>Overrides are parsed and <b>written after the definition's css</b> and allows developers to include arbitrary css inside the definition. Overrides are parsed as <b>LESS</b> files and all component variables are available inside an override file.</p>
  <p>Theme overrides are used to add css rules which are not available in the source definition, but are necessary for the theme to work.</p>
  <p>Site theme overrides are home to the <b>arbitrary</b> or <b>temporaneous</b> aspects of an element for integrating it on a site. Hacks, one-time fixes, shortcuts, etc are all sometimes important parts of making a website work, but aren't things we want to re-use from project to project. Using a <b>site override</b> file for an element, allows you to make these concessions without sullying the re-usability of the rest of your code.</p>

  <h5 class="ui header">CSS Write Order</h5>
  <div class="ui large bulleted list">
    <div class="item">
      CSS compiled from <code>src/definitions/elements/button.less</code>
    </div>
    <div class="item">
      CSS compiled from <code>src/themes/{themeName}/elements/button.overrides</code>
    </div>
    <div class="item">
      CSS compiled from <code>src/site/elements/button.overrides</code>
    </div>
  </div>

  <h3 class="ui header">Overrides in Practice</h3>
  <p>Some definitions files may even include override files as part of its default theme. This is to move the arbitrary bits outside of a definition. For example <code>ui icon</code> has the UTF content in its override file, so that themes do not inherit these arbitrary properties.</p>

  <div class="less code" data-type="LESS" data-title="src/themes/default/elements/icon.overrides">
    /*******************************
                Icons
    *******************************/

    /* Web Content */
    i.icon.search:before { content: "\f002"; }
    i.icon.mail.outline:before { content: "\f003"; }
    i.icon.external.link:before { content: "\f08e"; }
    i.icon.wifi:before { content: "\f012"; }
    i.icon.setting:before { content: "\f013"; }
    i.icon.home:before { content: "\f015"; }
    i.icon.inbox:before { content: "\f01c"; }
    i.icon.browser:before { content: "\f022"; }
    i.icon.tag:before { content: "\f02b"; }
    i.icon.tags:before { content: "\f02c"; }
    i.icon.calendar:before { content: "\f073"; }
    i.icon.comment:before { content: "\f075"; }
    i.icon.comments:before { content: "\f086"; }
    i.icon.shop:before { content: "\f07a"; }
    i.icon.privacy:before { content: "\f084"; }
    i.icon.settings:before { content: "\f085"; }
    i.icon.trophy:before { content: "\f091"; }
    i.icon.payment:before { content: "\f09d"; }
    i.icon.feed:before { content: "\f09e"; }
    i.icon.alarm.outline:before { content: "\f0a2"; }
    i.icon.tasks:before { content: "\f0ae"; }
    i.icon.cloud:before { content: "\f0c2"; }
    i.icon.lab:before { content: "\f0c3"; }
    i.icon.mail:before { content: "\f0e0"; }
    i.icon.idea:before { content: "\f0eb"; }
    i.icon.dashboard:before { content: "\f0e4"; }
    i.icon.sitemap:before { content: "\f0e8"; }
    i.icon.alarm:before { content: "\f0f3"; }
    i.icon.terminal:before { content: "\f120"; }
    i.icon.code:before { content: "\f121"; }
    i.icon.protect:before { content: "\f132"; }
    i.icon.calendar.outline:before { content: "\f133"; }
    i.icon.ticket:before { content: "\f145"; }
    i.icon.external.link.square:before { content: "\f14c"; }
    i.icon.map:before { content: "\f14e"; }
    i.icon.bug:before { content: "\f188"; }
    i.icon.mail.square:before { content: "\f199"; }
    i.icon.history:before { content: "\f1da"; }
    i.icon.options:before { content: "\f1de"; }
    i.icon.comment.outline:before { content: "\f0e5"; }
    i.icon.comments.outline:before { content: "\f0e6"; }

    /* User Actions */
    i.icon.download:before { content: "\f019"; }
    i.icon.repeat:before { content: "\f01e"; }
    i.icon.refresh:before { content: "\f021"; }
    i.icon.lock:before { content: "\f023"; }
    i.icon.bookmark:before { content: "\f02e"; }
    i.icon.print:before { content: "\f02f"; }
    i.icon.write:before { content: "\f040"; }
    i.icon.theme:before { content: "\f043"; }
    i.icon.adjust:before { content: "\f042"; }
    i.icon.edit:before { content: "\f044"; }
    i.icon.external.share:before { content: "\f045"; }
    i.icon.ban:before { content: "\f05e"; }
    i.icon.mail.forward:before { content: "\f064"; }
    i.icon.share:before { content: "\f064"; }
    i.icon.expand:before { content: "\f065"; }
    i.icon.compress:before { content: "\f066"; }
    i.icon.unhide:before { content: "\f06e"; }
    i.icon.hide:before { content: "\f070"; }
    i.icon.random:before { content: "\f074"; }
    i.icon.retweet:before { content: "\f079"; }
    i.icon.sign.out:before { content: "\f08b"; }
    i.icon.pin:before { content: "\f08d"; }
    i.icon.sign.in:before { content: "\f090"; }
    i.icon.upload:before { content: "\f093"; }
    i.icon.call:before { content: "\f095"; }
    i.icon.call.square:before { content: "\f098"; }
    i.icon.remove.bookmark:before { content: "\f097"; }
    i.icon.unlock:before { content: "\f09c"; }
    i.icon.configure:before { content: "\f0ad"; }
    i.icon.filter:before { content: "\f0b0"; }
    i.icon.wizard:before { content: "\f0d0"; }
    i.icon.undo:before { content: "\f0e2"; }
    i.icon.exchange:before { content: "\f0ec"; }
    i.icon.cloud.download:before { content: "\f0ed"; }
    i.icon.cloud.upload:before { content: "\f0ee"; }
    i.icon.reply:before { content: "\f112"; }
    i.icon.reply.all:before { content: "\f122"; }
    i.icon.erase:before { content: "\f12d"; }
    i.icon.unlock.alternate:before { content: "\f13e"; }
    i.icon.archive:before { content: "\f187"; }
    i.icon.translate:before { content: "\f1ab"; }
    i.icon.recycle:before { content: "\f1b8"; }
    i.icon.send:before { content: "\f1d8"; }
    i.icon.send.outline:before { content: "\f1d9"; }
    i.icon.share.alternate:before { content: "\f1e0"; }
    i.icon.share.alternate.square:before { content: "\f1e1"; }
    i.icon.wait:before { content: "\f017"; }
    i.icon.write.square:before { content: "\f14b"; }
    i.icon.share.square:before { content: "\f14d"; }

    /* Messages */
    i.icon.help.circle:before { content: "\f059"; }
    i.icon.info.circle:before { content: "\f05a"; }
    i.icon.warning:before { content: "\f12a"; }
    i.icon.warning.circle:before { content: "\f06a"; }
    i.icon.warning.sign:before { content: "\f071"; }
    i.icon.help:before { content: "\f128"; }
    i.icon.info:before { content: "\f129"; }
    i.icon.announcement:before { content: "\f0a1"; }

    /* Users */
    i.icon.users:before { content: "\f0c0"; }
    i.icon.doctor:before { content: "\f0f0"; }
    i.icon.female:before { content: "\f182"; }
    i.icon.male:before { content: "\f183"; }
    i.icon.child:before { content: "\f1ae"; }
    i.icon.user:before { content: "\f007"; }
    i.icon.handicap:before { content: "\f193"; }
    i.icon.student:before { content: "\f19d"; }

    /* View Adjustment */
    i.icon.grid.layout:before { content: "\f00a"; }
    i.icon.list.layout:before { content: "\f00b"; }
    i.icon.block.layout:before { content: "\f009"; }
    i.icon.zoom:before { content: "\f00e"; }
    i.icon.zoom.out:before { content: "\f010"; }
    i.icon.resize.vertical:before { content: "\f07d"; }
    i.icon.resize.horizontal:before { content: "\f07e"; }
    i.icon.maximize:before { content: "\f0b2"; }
    i.icon.crop:before { content: "\f125"; }

    /* Literal Objects */
    i.icon.cocktail:before { content: "\f000"; }
    i.icon.road:before { content: "\f018"; }
    i.icon.flag:before { content: "\f024"; }
    i.icon.book:before { content: "\f02d"; }
    i.icon.gift:before { content: "\f06b"; }
    i.icon.leaf:before { content: "\f06c"; }
    i.icon.fire:before { content: "\f06d"; }
    i.icon.plane:before { content: "\f072"; }
    i.icon.magnet:before { content: "\f076"; }
    i.icon.legal:before { content: "\f0e3"; }
    i.icon.lemon:before { content: "\f094"; }
    i.icon.world:before { content: "\f0ac"; }
    i.icon.travel:before { content: "\f0b1"; }
    i.icon.shipping:before { content: "\f0d1"; }
    i.icon.money:before { content: "\f0d6"; }
    i.icon.lightning:before { content: "\f0e7"; }
    i.icon.rain:before { content: "\f0e9"; }
    i.icon.treatment:before { content: "\f0f1"; }
    i.icon.suitcase:before { content: "\f0f2"; }
    i.icon.bar:before { content: "\f0fc"; }
    i.icon.flag.outline:before { content: "\f11d"; }
    i.icon.flag.checkered:before { content: "\f11e"; }
    i.icon.puzzle:before { content: "\f12e"; }
    i.icon.fire.extinguisher:before { content: "\f134"; }
    i.icon.rocket:before { content: "\f135"; }
    i.icon.anchor:before { content: "\f13d"; }
    i.icon.bullseye:before { content: "\f140"; }
    i.icon.sun:before { content: "\f185"; }
    i.icon.moon:before { content: "\f186"; }
    i.icon.fax:before { content: "\f1ac"; }
    i.icon.life.ring:before { content: "\f1cd"; }
    i.icon.bomb:before { content: "\f1e2"; }

    /* Shapes */
    i.icon.crosshairs:before { content: "\f05b"; }
    i.icon.asterisk:before { content: "\f069"; }
    i.icon.certificate:before { content: "\f0a3"; }
    i.icon.circle:before { content: "\f111"; }
    i.icon.quote.left:before { content: "\f10d"; }
    i.icon.quote.right:before { content: "\f10e"; }
    i.icon.ellipsis.horizontal:before { content: "\f141"; }
    i.icon.ellipsis.vertical:before { content: "\f142"; }
    i.icon.cube:before { content: "\f1b2"; }
    i.icon.cubes:before { content: "\f1b3"; }
    i.icon.circle.notched:before { content: "\f1ce"; }
    i.icon.circle.thin:before { content: "\f1db"; }

    /* Item Selection */
    i.icon.checkmark:before { content: "\f00c"; }
    i.icon.remove:before { content: "\f00d"; }
    i.icon.checkmark.box:before { content: "\f046"; }
    i.icon.move:before { content: "\f047"; }
    i.icon.add.circle:before { content: "\f055"; }
    i.icon.minus.circle:before { content: "\f056"; }
    i.icon.remove.circle:before { content: "\f057"; }
    i.icon.check.circle:before { content: "\f058"; }
    i.icon.remove.circle.outline:before { content: "\f05c"; }
    i.icon.check.circle.outline:before { content: "\f05d"; }
    i.icon.plus:before { content: "\f067"; }
    i.icon.minus:before { content: "\f068"; }
    i.icon.add.square:before { content: "\f0fe"; }
    i.icon.radio:before { content: "\f10c"; }
    i.icon.selected.radio:before { content: "\f192"; }
    i.icon.minus.square:before { content: "\f146"; }
    i.icon.minus.square.outline:before { content: "\f147"; }
    i.icon.check.square:before { content: "\f14a"; }
    i.icon.plus.square.outline:before { content: "\f196"; }

    /* Media */
    i.icon.film:before { content: "\f008"; }
    i.icon.sound:before { content: "\f025"; }
    i.icon.photo:before { content: "\f030"; }
    i.icon.bar.chart:before { content: "\f080"; }
    i.icon.camera.retro:before { content: "\f083"; }

    /* Pointers */
    i.icon.arrow.circle.outline.down:before { content: "\f01a"; }
    i.icon.arrow.circle.outline.up:before { content: "\f01b"; }
    i.icon.chevron.left:before { content: "\f053"; }
    i.icon.chevron.right:before { content: "\f054"; }
    i.icon.arrow.left:before { content: "\f060"; }
    i.icon.arrow.right:before { content: "\f061"; }
    i.icon.arrow.up:before { content: "\f062"; }
    i.icon.arrow.down:before { content: "\f063"; }
    i.icon.chevron.up:before { content: "\f077"; }
    i.icon.chevron.down:before { content: "\f078"; }
    i.icon.pointing.right:before { content: "\f0a4"; }
    i.icon.pointing.left:before { content: "\f0a5"; }
    i.icon.pointing.up:before { content: "\f0a6"; }
    i.icon.pointing.down:before { content: "\f0a7"; }
    i.icon.arrow.circle.left:before { content: "\f0a8"; }
    i.icon.arrow.circle.right:before { content: "\f0a9"; }
    i.icon.arrow.circle.up:before { content: "\f0aa"; }
    i.icon.arrow.circle.down:before { content: "\f0ab"; }
    i.icon.caret.down:before { content: "\f0d7"; }
    i.icon.caret.up:before { content: "\f0d8"; }
    i.icon.caret.left:before { content: "\f0d9"; }
    i.icon.caret.right:before { content: "\f0da"; }
    i.icon.angle.double.left:before { content: "\f100"; }
    i.icon.angle.double.right:before { content: "\f101"; }
    i.icon.angle.double.up:before { content: "\f102"; }
    i.icon.angle.double.down:before { content: "\f103"; }
    i.icon.angle.left:before { content: "\f104"; }
    i.icon.angle.right:before { content: "\f105"; }
    i.icon.angle.up:before { content: "\f106"; }
    i.icon.angle.down:before { content: "\f107"; }
    i.icon.chevron.circle.left:before { content: "\f137"; }
    i.icon.chevron.circle.right:before { content: "\f138"; }
    i.icon.chevron.circle.up:before { content: "\f139"; }
    i.icon.chevron.circle.down:before { content: "\f13a"; }
    i.icon.toggle.down:before { content: "\f150"; }
    i.icon.toggle.up:before { content: "\f151"; }
    i.icon.toggle.right:before { content: "\f152"; }
    i.icon.long.arrow.down:before { content: "\f175"; }
    i.icon.long.arrow.up:before { content: "\f176"; }
    i.icon.long.arrow.left:before { content: "\f177"; }
    i.icon.long.arrow.right:before { content: "\f178"; }
    i.icon.arrow.circle.outline.right:before { content: "\f18e"; }
    i.icon.arrow.circle.outline.left:before { content: "\f190"; }
    i.icon.toggle.left:before { content: "\f191"; }

    /* Computer */
    i.icon.power:before { content: "\f011"; }
    i.icon.trash:before { content: "\f014"; }
    i.icon.disk.outline:before { content: "\f0a0"; }
    i.icon.desktop:before { content: "\f108"; }
    i.icon.laptop:before { content: "\f109"; }
    i.icon.tablet:before { content: "\f10a"; }
    i.icon.mobile:before { content: "\f10b"; }
    i.icon.game:before { content: "\f11b"; }
    i.icon.keyboard:before { content: "\f11c"; }

    /* File System */
    i.icon.folder:before { content: "\f07b"; }
    i.icon.folder.open:before { content: "\f07c"; }
    i.icon.level.up:before { content: "\f148"; }
    i.icon.level.down:before { content: "\f149"; }
    i.icon.file:before { content: "\f15b"; }
    i.icon.file.outline:before { content: "\f016"; }
    i.icon.file.text:before { content: "\f15c"; }
    i.icon.file.text.outline:before { content: "\f0f6"; }
    i.icon.folder.outline:before { content: "\f114"; }
    i.icon.folder.open.outline:before { content: "\f115"; }
    i.icon.file.pdf.outline:before { content: "\f1c1"; }
    i.icon.file.word.outline:before { content: "\f1c2"; }
    i.icon.file.excel.outline:before { content: "\f1c3"; }
    i.icon.file.powerpoint.outline:before { content: "\f1c4"; }
    i.icon.file.image.outline:before { content: "\f1c5"; }
    i.icon.file.archive.outline:before { content: "\f1c6"; }
    i.icon.file.audio.outline:before { content: "\f1c7"; }
    i.icon.file.video.outline:before { content: "\f1c8"; }
    i.icon.file.code.outline:before { content: "\f1c9"; }

    /* Technologies */
    i.icon.barcode:before { content: "\f02a"; }
    i.icon.qrcode:before { content: "\f029"; }
    i.icon.fork:before { content: "\f126"; }
    i.icon.html5:before { content: "\f13b"; }
    i.icon.css3:before { content: "\f13c"; }
    i.icon.rss.square:before { content: "\f143"; }
    i.icon.openid:before { content: "\f19b"; }
    i.icon.database:before { content: "\f1c0"; }

    /* Rating */
    i.icon.heart:before { content: "\f004"; }
    i.icon.star:before { content: "\f005"; }
    i.icon.empty.star:before { content: "\f006"; }
    i.icon.thumbs.outline.up:before { content: "\f087"; }
    i.icon.thumbs.outline.down:before { content: "\f088"; }
    i.icon.star.half:before { content: "\f089"; }
    i.icon.empty.heart:before { content: "\f08a"; }
    i.icon.smile:before { content: "\f118"; }
    i.icon.frown:before { content: "\f119"; }
    i.icon.meh:before { content: "\f11a"; }
    i.icon.star.half.empty:before { content: "\f123"; }
    i.icon.thumbs.up:before { content: "\f164"; }
    i.icon.thumbs.down:before { content: "\f165"; }

    /* Audio */
    i.icon.music:before { content: "\f001"; }
    i.icon.video.play.outline:before { content: "\f01d"; }
    i.icon.volume.off:before { content: "\f026"; }
    i.icon.volume.down:before { content: "\f027"; }
    i.icon.volume.up:before { content: "\f028"; }
    i.icon.record:before { content: "\f03d"; }
    i.icon.step.backward:before { content: "\f048"; }
    i.icon.fast.backward:before { content: "\f049"; }
    i.icon.backward:before { content: "\f04a"; }
    i.icon.play:before { content: "\f04b"; }
    i.icon.pause:before { content: "\f04c"; }
    i.icon.stop:before { content: "\f04d"; }
    i.icon.forward:before { content: "\f04e"; }
    i.icon.fast.forward:before { content: "\f050"; }
    i.icon.step.forward:before { content: "\f051"; }
    i.icon.eject:before { content: "\f052"; }
    i.icon.unmute:before { content: "\f130"; }
    i.icon.mute:before { content: "\f131"; }
    i.icon.video.play:before { content: "\f144"; }


    /* Map & Locations */
    i.icon.marker:before { content: "\f041"; }
    i.icon.coffee:before { content: "\f0f4"; }
    i.icon.food:before { content: "\f0f5"; }
    i.icon.building.outline:before { content: "\f0f7"; }
    i.icon.hospital:before { content: "\f0f8"; }
    i.icon.emergency:before { content: "\f0f9"; }
    i.icon.first.aid:before { content: "\f0fa"; }
    i.icon.military:before { content: "\f0fb"; }
    i.icon.h:before { content: "\f0fd"; }
    i.icon.location.arrow:before { content: "\f124"; }
    i.icon.space.shuttle:before { content: "\f197"; }
    i.icon.university:before { content: "\f19c"; }
    i.icon.building:before { content: "\f1ad"; }
    i.icon.paw:before { content: "\f1b0"; }
    i.icon.spoon:before { content: "\f1b1"; }
    i.icon.car:before { content: "\f1b9"; }
    i.icon.taxi:before { content: "\f1ba"; }
    i.icon.tree:before { content: "\f1bb"; }

    /* Tables */
    i.icon.table:before { content: "\f0ce"; }
    i.icon.columns:before { content: "\f0db"; }
    i.icon.sort:before { content: "\f0dc"; }
    i.icon.sort.ascending:before { content: "\f0dd"; }
    i.icon.sort.descending:before { content: "\f0de"; }
    i.icon.sort.alphabet.ascending:before { content: "\f15d"; }
    i.icon.sort.alphabet.descending:before { content: "\f15e"; }
    i.icon.sort.content.ascending:before { content: "\f160"; }
    i.icon.sort.content.descending:before { content: "\f161"; }
    i.icon.sort.numeric.ascending:before { content: "\f162"; }
    i.icon.sort.numeric.descending:before { content: "\f163"; }

    /* Text Editor */
    i.icon.font:before { content: "\f031"; }
    i.icon.bold:before { content: "\f032"; }
    i.icon.italic:before { content: "\f033"; }
    i.icon.text.height:before { content: "\f034"; }
    i.icon.text.width:before { content: "\f035"; }
    i.icon.align.left:before { content: "\f036"; }
    i.icon.align.center:before { content: "\f037"; }
    i.icon.align.right:before { content: "\f038"; }
    i.icon.align.justify:before { content: "\f039"; }
    i.icon.list:before { content: "\f03a"; }
    i.icon.outdent:before { content: "\f03b"; }
    i.icon.indent:before { content: "\f03c"; }
    i.icon.linkify:before { content: "\f0c1"; }
    i.icon.cut:before { content: "\f0c4"; }
    i.icon.copy:before { content: "\f0c5"; }
    i.icon.attach:before { content: "\f0c6"; }
    i.icon.save:before { content: "\f0c7"; }
    i.icon.content:before { content: "\f0c9"; }
    i.icon.unordered.list:before { content: "\f0ca"; }
    i.icon.ordered.list:before { content: "\f0cb"; }
    i.icon.strikethrough:before { content: "\f0cc"; }
    i.icon.underline:before { content: "\f0cd"; }
    i.icon.paste:before { content: "\f0ea"; }
    i.icon.unlink:before { content: "\f127"; }
    i.icon.superscript:before { content: "\f12b"; }
    i.icon.subscript:before { content: "\f12c"; }
    i.icon.header:before { content: "\f1dc"; }
    i.icon.paragraph:before { content: "\f1dd"; }

    /* Currency */
    i.icon.euro:before { content: "\f153"; }
    i.icon.pound:before { content: "\f154"; }
    i.icon.dollar:before { content: "\f155"; }
    i.icon.rupee:before { content: "\f156"; }
    i.icon.yen:before { content: "\f157"; }
    i.icon.ruble:before { content: "\f158"; }
    i.icon.won:before { content: "\f159"; }
    i.icon.lira:before { content: "\f195"; }

    /* Networks and Websites*/
    i.icon.twitter.square:before { content: "\f081"; }
    i.icon.facebook.square:before { content: "\f082"; }
    i.icon.linkedin.square:before { content: "\f08c"; }
    i.icon.github.square:before { content: "\f092"; }
    i.icon.twitter:before { content: "\f099"; }
    i.icon.facebook:before { content: "\f09a"; }
    i.icon.github:before { content: "\f09b"; }
    i.icon.pinterest:before { content: "\f0d2"; }
    i.icon.pinterest.square:before { content: "\f0d3"; }
    i.icon.google.plus.square:before { content: "\f0d4"; }
    i.icon.google.plus:before { content: "\f0d5"; }
    i.icon.linkedin:before { content: "\f0e1"; }
    i.icon.github.alternate:before { content: "\f113"; }
    i.icon.maxcdn:before { content: "\f136"; }
    i.icon.bitcoin:before { content: "\f15a"; }
    i.icon.youtube.square:before { content: "\f166"; }
    i.icon.youtube:before { content: "\f167"; }
    i.icon.xing:before { content: "\f168"; }
    i.icon.xing.square:before { content: "\f169"; }
    i.icon.youtube.play:before { content: "\f16a"; }
    i.icon.dropbox:before { content: "\f16b"; }
    i.icon.stack.overflow:before { content: "\f16c"; }
    i.icon.instagram:before { content: "\f16d"; }
    i.icon.flickr:before { content: "\f16e"; }
    i.icon.adn:before { content: "\f170"; }
    i.icon.bitbucket:before { content: "\f171"; }
    i.icon.bitbucket.square:before { content: "\f172"; }
    i.icon.tumblr:before { content: "\f173"; }
    i.icon.tumblr.square:before { content: "\f174"; }
    i.icon.apple:before { content: "\f179"; }
    i.icon.windows:before { content: "\f17a"; }
    i.icon.android:before { content: "\f17b"; }
    i.icon.linux:before { content: "\f17c"; }
    i.icon.dribbble:before { content: "\f17d"; }
    i.icon.skype:before { content: "\f17e"; }
    i.icon.foursquare:before { content: "\f180"; }
    i.icon.trello:before { content: "\f181"; }
    i.icon.gittip:before { content: "\f184"; }
    i.icon.vk:before { content: "\f189"; }
    i.icon.weibo:before { content: "\f18a"; }
    i.icon.renren:before { content: "\f18b"; }
    i.icon.pagelines:before { content: "\f18c"; }
    i.icon.stack.exchange:before { content: "\f18d"; }
    i.icon.vimeo:before { content: "\f194"; }
    i.icon.slack:before { content: "\f198"; }
    i.icon.wordpress:before { content: "\f19a"; }
    i.icon.yahoo:before { content: "\f19e"; }
    i.icon.google:before { content: "\f1a0"; }
    i.icon.reddit:before { content: "\f1a1"; }
    i.icon.reddit.square:before { content: "\f1a2"; }
    i.icon.stumbleupon.circle:before { content: "\f1a3"; }
    i.icon.stumbleupon:before { content: "\f1a4"; }
    i.icon.delicious:before { content: "\f1a5"; }
    i.icon.digg:before { content: "\f1a6"; }
    i.icon.pied.piper:before { content: "\f1a7"; }
    i.icon.pied.piper.alternate:before { content: "\f1a8"; }
    i.icon.drupal:before { content: "\f1a9"; }
    i.icon.joomla:before { content: "\f1aa"; }
    i.icon.behance:before { content: "\f1b4"; }
    i.icon.behance.square:before { content: "\f1b5"; }
    i.icon.steam:before { content: "\f1b6"; }
    i.icon.steam.square:before { content: "\f1b7"; }
    i.icon.spotify:before { content: "\f1bc"; }
    i.icon.deviantart:before { content: "\f1bd"; }
    i.icon.soundcloud:before { content: "\f1be"; }
    i.icon.vine:before { content: "\f1ca"; }
    i.icon.codepen:before { content: "\f1cb"; }
    i.icon.jsfiddle:before { content: "\f1cc"; }
    i.icon.rebel:before { content: "\f1d0"; }
    i.icon.empire:before { content: "\f1d1"; }
    i.icon.git.square:before { content: "\f1d2"; }
    i.icon.git:before { content: "\f1d3"; }
    i.icon.hacker.news:before { content: "\f1d4"; }
    i.icon.tencent.weibo:before { content: "\f1d5"; }
    i.icon.qq:before { content: "\f1d6"; }
    i.icon.wechat:before { content: "\f1d7"; }

    /*******************************
                Aliases
    *******************************/

    i.icon.like:before { content: "\f004"; }
    i.icon.favorite:before { content: "\f005"; }
    i.icon.video:before { content: "\f008"; }
    i.icon.check:before { content: "\f00c"; }
    i.icon.remove:before { content: "\f00d"; }
    i.icon.close:before { content: "\f00d"; }
    i.icon.cancel:before { content: "\f00d"; }
    i.icon.delete:before { content: "\f00d"; }
    i.icon.x:before { content: "\f00d"; }
    i.icon.zoom.in:before { content: "\f00e"; }
    i.icon.magnify:before { content: "\f00e"; }
    i.icon.shutdown:before { content: "\f011"; }
    i.icon.signal:before { content: "\f012"; }
    i.icon.clock:before { content: "\f017"; }
    i.icon.time:before { content: "\f017"; }
    i.icon.play.circle.outline:before { content: "\f01d"; }
    i.icon.clockwise:before { content: "\f01e"; }
    i.icon.headphone:before { content: "\f025"; }
    i.icon.volume.off:before { content: "\f026"; }
    i.icon.camera:before { content: "\f030"; }
    i.icon.video.camera:before { content: "\f03d"; }
    i.icon.picture:before { content: "\f03e"; }
    i.icon.pencil:before { content: "\f040"; }
    i.icon.compose:before { content: "\f040"; }
    i.icon.point:before { content: "\f041"; }
    i.icon.tint:before { content: "\f043"; }
    i.icon.signup:before { content: "\f044"; }
    i.icon.plus.circle:before { content: "\f055"; }
    i.icon.minus.circle:before { content: "\f056"; }
    i.icon.dont:before { content: "\f05e"; }
    i.icon.minimize:before { content: "\f066"; }
    i.icon.add:before { content: "\f067"; }
    i.icon.eye:before { content: "\f06e"; }
    i.icon.attention:before { content: "\f06a"; }
    i.icon.cart:before { content: "\f07a"; }
    i.icon.plane:before { content: "\f072"; }
    i.icon.shuffle:before { content: "\f074"; }
    i.icon.talk:before { content: "\f075"; }
    i.icon.chat:before { content: "\f075"; }
    i.icon.shopping.cart:before { content: "\f07a"; }
    i.icon.bar.graph:before { content: "\f080"; }
    i.icon.key:before { content: "\f084"; }
    i.icon.privacy:before { content: "\f084"; }
    i.icon.cogs:before { content: "\f085"; }
    i.icon.discussions:before { content: "\f086"; }
    i.icon.like.outline:before { content: "\f087"; }
    i.icon.dislike.outline:before { content: "\f088"; }
    i.icon.heart.outline:before { content: "\f08a"; }
    i.icon.log.out:before { content: "\f08b"; }
    i.icon.thumb.tack:before { content: "\f08d"; }
    i.icon.winner:before { content: "\f091"; }
    i.icon.bookmark.outline:before { content: "\f097"; }
    i.icon.phone.square:before { content: "\f098"; }
    i.icon.phone.square:before { content: "\f098"; }
    i.icon.credit.card:before { content: "\f09d"; }
    i.icon.rss:before { content: "\f09e"; }
    i.icon.hdd.outline:before { content: "\f0a0"; }
    i.icon.bullhorn:before { content: "\f0a1"; }
    i.icon.bell:before { content: "\f0f3"; }
    i.icon.hand.outline.right:before { content: "\f0a4"; }
    i.icon.hand.outline.left:before { content: "\f0a5"; }
    i.icon.hand.outline.up:before { content: "\f0a6"; }
    i.icon.hand.outline.down:before { content: "\f0a7"; }
    i.icon.globe:before { content: "\f0ac"; }
    i.icon.wrench:before { content: "\f0ad"; }
    i.icon.briefcase:before { content: "\f0b1"; }
    i.icon.group:before { content: "\f0c0"; }
    i.icon.flask:before { content: "\f0c3"; }
    i.icon.sidebar:before { content: "\f0c9"; }
    i.icon.bars:before { content: "\f0c9"; }
    i.icon.list.ul:before { content: "\f0ca"; }
    i.icon.list.ol:before { content: "\f0cb"; }
    i.icon.numbered.list:before { content: "\f0cb"; }
    i.icon.magic:before { content: "\f0d0"; }
    i.icon.truck:before { content: "\f0d1"; }
    i.icon.currency:before { content: "\f0d6"; }
    i.icon.triangle.down:before { content: "\f0d7"; }
    i.icon.dropdown:before { content: "\f0d7"; }
    i.icon.triangle.up:before { content: "\f0d8"; }
    i.icon.triangle.left:before { content: "\f0d9"; }
    i.icon.triangle.right:before { content: "\f0da"; }
    i.icon.envelope:before { content: "\f0e0"; }
    i.icon.conversation:before { content: "\f0e6"; }
    i.icon.lightning:before { content: "\f0e7"; }
    i.icon.umbrella:before { content: "\f0e9"; }
    i.icon.lightbulb:before { content: "\f0eb"; }
    i.icon.suitcase:before { content: "\f0f2"; }
    i.icon.bell.outline:before { content: "\f0a2"; }
    i.icon.ambulance:before { content: "\f0f9"; }
    i.icon.medkit:before { content: "\f0fa"; }
    i.icon.fighter.jet:before { content: "\f0fb"; }
    i.icon.beer:before { content: "\f0fc"; }
    i.icon.plus.square:before { content: "\f0fe"; }
    i.icon.computer:before { content: "\f108"; }
    i.icon.circle.outline:before { content: "\f10c"; }
    i.icon.spinner:before { content: "\f110"; }
    i.icon.gamepad:before { content: "\f11b"; }
    i.icon.star.half.full:before { content: "\f123"; }
    i.icon.remove.link:before { content: "\f127"; }
    i.icon.question:before { content: "\f128"; }
    i.icon.attention:before { content: "\f12a"; }
    i.icon.eraser:before { content: "\f12d"; }
    i.icon.microphone:before { content: "\f130"; }
    i.icon.microphone.slash:before { content: "\f131"; }
    i.icon.shield:before { content: "\f132"; }
    i.icon.target:before { content: "\f140"; }
    i.icon.play.circle:before { content: "\f144"; }
    i.icon.pencil.square:before { content: "\f14b"; }
    i.icon.compass:before { content: "\f14e"; }
    i.icon.eur:before { content: "\f153"; }
    i.icon.gbp:before { content: "\f154"; }
    i.icon.usd:before { content: "\f155"; }
    i.icon.inr:before { content: "\f156"; }
    i.icon.cny:before,
    i.icon.rmb:before,
    i.icon.jpy:before { content: "\f157"; }
    i.icon.rouble:before,
    i.icon.rub:before { content: "\f158"; }
    i.icon.won:before,
    i.icon.krw:before { content: "\f159"; }
    i.icon.btc:before { content: "\f15a"; }
    i.icon.try:before { content: "\f195"; }
    i.icon.zip:before { content: "\f187"; }
    i.icon.dot.circle.outline:before { content: "\f192"; }

    i.icon.sliders:before { content: "\f1de"; }
    i.icon.graduation:before { content: "\f19d"; }
    i.icon.\33d:before { content: "\f1b2"; }
    i.icon.weixin:before { content: "\f1d7"; }
  </div>

  <h2 class="ui header">Creating Themes</h2>

  <h3 class="ui header">A Practical Example</h3>
  <p>Perhaps you find it useful while working on your site to have icons aliases in your local language <b>Spanish</b> to make them easier to remember. You might include a set of aliases in your site's icon overrides in  <code>src/site/elements/icon.overrides</code>.</p>
  <p>These files already exist for your project, but are left blank by default. You can simply update the file with your aliases and save it and <code>gulp watch</code> will automatically recreate the original definition with your changes.</p>
  <div class="less code" data-type="LESS" data-title="src/site/elements/icon.overrides">
    /* Alias Search in Spanish */
    i.icon.buscar:before { content: "\f002"; }
  </div>

  <h3 class="ui header">Creating Packaged Themes</h3>
  <p>After finishing up work on your project, you realize that all of your icon aliases you created might be useful to other Spanish developers working with Semantic. You can then create a packaged theme for distribution that other people can download and use on their site</p>
  <p>To do this create a new folder under themes with your theme name, for example <code>src/themes/spanish/</code> and add your variables and overrides file. Keep in mind all themes must include <b>both</b> an override and variable file, if no variables are changed you can include a blank <code>.variables</code> file.</p>

  <p>You can test your packaged theme locally by adjusting your <code>theme.config</code> to use the specified theme:</p>
  <div class="less code" data-type="LESS" data-title="src/theme.config" data-type="less">
    /*******************************
                Themes
    *******************************/

    /* Global */
    @site        : 'default';
    @reset       : 'default';

    /* Elements */
    @button      : 'default';
    @container   : 'default';
    @icon        : 'spanish';
  </div>

  <div class="ui warning message">A package manager for distributing semantic themes is in the works, but does not yet exist. Please check back for more information.</div>

  <h3 class="ui header">Variables in Semantic</h3>

  <p>Variables are not just one-to-one matches with css properties, but let you work with higher-order concepts in an element's design, that may adjust several properties at once.</p>

  <h4 class="ui header">Abstracting Concepts to Remove Tedium</h4>
  <p>Sometimes variables are used to deal with latent issues in CSS. For example <code>@lineHeight</code> might seem like a simple value. Setting a line-height greater than 1 on an input is necessary to make sure descenders like "p" or "q" aren't cut off in your form. Some browsers even implicitly add this line-height to inputs even if you specify a value to low.</p>
  <p>Having a different line height on input elements increases its vertical padding to a larger value than what is set in <code>@verticalPadding</code>. This implicit change in actual vertical-padding on an input, would mean the element would not line up with other UI elements that use the same <code>@verticalPadding</code>. Semantic deals with this on a framework level, by using derived values for padding specifically on inputs.</p>
  <div class="less code" data-title="src/themes/default/elements/input.variables" data-type="less">
    @lineHeight: 1.2em;
    @lineHeightOffset: ((@lineHeight - 1em) / 2);
    @padding: (@verticalPadding - @lineHeightOffset) @horizontalPadding;
  </div>

  <p>Using a <code>@lineHeightOffset</code> is also useful for other unexpected css quirks.

  <p>For example floated elements do not receive the same top padding as other sibling content:</p>
  <div class="less code" data-title="src/themes/default/collections/menu.variables" data-type="less">
  @menuIconFloat: right;
  @menuIconMargin: @lineHeightOffset 0em 0em 1em;
  </div>
  <p>Or headers might appear overly spaced because they have additional vertical padding from large line heights.</p>
  <div class="less code" data-title="src/themes/default/elements/header.variables" data-type="less">
  /* Space exactly 2rem */
  @topMargin: ~"calc(2rem - "@lineHeightOffset~")";
  </div>

  <h4 class="ui header">Abstracting Concepts to Facilitate Theming</h4>
  <p>Sometimes there is a disconnect between the name of a css property, and the function it performs visually, or a single property might house multiple concepts. For example a button may have a <code>@shadow</code> to make it appear raised, but it might also use require an inset box shadow to give the button a <code>border</code> that can use the shade of an element's background color. That single <code>box-shadow</code> definition might actually houses several separate concepts.</p>

  <p>Semantic does its best to abstract out each concept separately when possible.</p>

  <div class="less code" data-title="src/themes/default/elements/button.variables" data-type="less">
    /* Internal Shadow */
    @shadowDistance: 0em;
    @shadowOffset: (@shadowDistance / 2);
    @shadowBoxShadow: 0px -@shadowDistance 0px 0px @borderColor inset;

    /* Box Shadow */
    @borderBoxShadowColor: transparent;
    @borderBoxShadowWidth: 1px;
    @borderBoxShadow: 0px 0px 0px @borderBoxShadowWidth @borderBoxShadowColor inset;
    @boxShadow:
      @borderBoxShadow,
      @shadowBoxShadow
    ;
    /* Remove Border on Colored */
    @coloredBoxShadow: @shadowBoxShadow;

  </div>

  <p>This may seem like way too much abstraction, but its important to note that themes <b>do not need to redefine all these derived variables</b>. For example, the "raised" theme, just redefines a single variable, which modifies the four or five other derived variables that the theme maker does not even need to know exist.</p>
  <div class="less code" data-title="src/themes/raised/elements/button.variables">
    @shadowDistance: 0.3em;
  </div>

  <h2 class="ui header">Extending Semantic</h2>

  <p>Writing definitions while designing new interface elements is similar to <a href="http://en.wikipedia.org/wiki/Test-driven_development">test driven development</a> when writing code. Definitions are a rubric for all possible ways an element can appear visually.</p>

  <p>Creating UI definitions lets you create components that are <b>self documenting</b> so that other team-members working on your project can develop with immediately without spending time learning internal naming conventions.</p>


</div>