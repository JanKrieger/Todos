---
title: A guide for the Meteor ToDo App
author: Jan Krieger
ID: 1810640043

---

<p><a href="https://www.fh-burgenland.at"><img src="https://www.fh-burgenland.at/typo3conf/ext/fh_burgenland/Resources/Public/Images/fh-burgenland-logo.png" alt="N|Solid"></a></p>
<h1 id="meteor-todo-application---installationsleitfaden">Meteor ToDo Application - Installationsleitfaden</h1>
<h2 id="allgemeines">Allgemeines</h2>
<p>Die Applikation ist unter folgendem Link erreichbar: <a href="https://jk-simple-todos.herokuapp.com">https://jk-simple-todos.herokuapp.com</a></p>
<h2 id="lokale-installation-von-meteor">Lokale Installation von Meteor</h2>
<h3 id="installation-unter-windows">Installation unter Windows</h3>
<h4 id="download-von-chocolatey">Download von Chocolatey</h4>
<p>Powershell (oder Windows-Terminal) als Administrator starten und folgenden Befehl ausführen, um Chocolatey herunterzuladen:</p>
<pre><code>Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
</code></pre>
<p>Im Anschluss starten wir sicherheitshalber die Shell neu.</p>
<h4 id="download-von-meteor">Download von Meteor</h4>
<p>In der neu geöffneten (Admin-) Shell installieren wir mittels</p>
<pre><code>choco install meteor
</code></pre>
<p>nun Meteor auf dem Computer und bestätigen in diesem Installationsschritt die Frage ob das Meteor-Package das Script “chocolateyinstall.ps1” ausführen darf mit ja (Y).<br>
Nach etwas Geduld erscheint im besten Fall die Erfolgsmeldung der Installation:<img src="https://i.ibb.co/Zghb6xg/Meteor-success.png" alt="You did it"></p>
<h3 id="erstellen-der-todo-app">Erstellen der ToDo-App</h3>
<p>Im Anschluss starten wir sicherheitshalber die Shell neu und erstellen mittels</p>
<pre><code>meteor create simple-todos
</code></pre>
<p>die ToDo-Application. Auch dieser Schritt bedarf etwas Geduld.<br>
Sobald der Ordner und die Files angelegt sind, navigieren wir in den Ordner<br>
und starten die neu erstellte App.</p>
<pre><code>cd simple-todos
meteor
</code></pre>
<p>Unter Umständen (je nach verwendetem Anti-Viren Programm und der verwendeten Firewall) muss die Kommunikation noch erlaubt werden<br>
<img src="https://i.ibb.co/wCBVDcx/meteor-firewall.png" alt="enter image description here"></p>
<p>Wenn auch dies ohne Fehler von Statten ging kann im Webbrowser die Meteor-App aufgerufen werden:</p>
<pre><code>http://localhost:3000
</code></pre>
<p><img src="https://i.ibb.co/5nQSjjT/Meteor-todo.png" alt="enter image description here"></p>
<h3 id="individualisierung-der-todo-app">Individualisierung der ToDo App</h3>
<p>Anschließend wechseln wir in das Verzeichnis der Todo-App (unter Windows finden wir dies in der Regel unter C:\simple-todos\ und öffnen im Unterordner “client” die <code>main.html</code> Datei mit einem Editor (hier wird Notepad++) verwendet.</p>
<p>Wir passen den Title-Tag an und fügen hier den gewünschten Namen ein (Rubidogs ToDo App),</p>
<pre><code>&lt;head&gt;
  &lt;title&gt;Rubidogs ToDo App&lt;/title&gt;
&lt;/head&gt;
</code></pre>
<p>Wir erweitern unsere Ordnerstruktur im Ordner C:\simple-todos\ um die Unterordner “imports”, sowie darin den Ordner “ui” und erstellen in diesem die files <code>body.html</code> und <code>body.js</code> mit dem folgenden Code:</p>
<h4 id="body.html">body.html:</h4>
<pre><code>   &lt;body&gt;
    &lt;div class="container"&gt;
      &lt;header&gt;
        &lt;h1&gt;Todo List&lt;/h1&gt;
      &lt;/header&gt;
      &lt;ul&gt;
        {{#each tasks}}
          {{&gt; task}}
        {{/each}}
      &lt;/ul&gt;
    &lt;/div&gt;
  &lt;/body&gt;
  &lt;template name="task"&gt;
    &lt;li&gt;{{text}}&lt;/li&gt;
  &lt;/template&gt;
</code></pre>
<h4 id="body.js">body.js</h4>
<pre><code>import { Template } from 'meteor/templating';
import './body.html';
Template.body.helpers({
  tasks: [
    { text: 'This is task 1' },
    { text: 'This is task 2' },
    { text: 'This is task 3' },
  ],
});
</code></pre>
<p>Abschließend löschen wir aus dem File <code>main.js</code> den Code heraus und fügen lediglich</p>
<pre><code>import '../imports/ui/body.js';
</code></pre>
<p>ein.</p>
<p>Ebenso wird mit der <code>main.html</code> verfahren, sodass dort nur der Titel der Seite stehen bleibt (siehe oben).</p>
<h4 id="farbe-ins-spiel-bringen">Farbe ins Spiel bringen</h4>
<p>im Client-Ordner legen passen wir das File <code>main.css</code> an und fügen folgenden Code ein:</p>
<pre><code>body {
  font-family: sans-serif;
  background-color: #F9F97E;
  background-image: linear-gradient(to bottom, #F9F97E, white 100%);
  background-attachment: fixed;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 0;
  margin: 0;
  font-size: 14px;
}
.container {
  max-width: 600px;
  margin: 0 auto;
  min-height: 100%;
  background: white;
} 
header {
  background: #d2edf4;
  background-image: linear-gradient(to bottom,#FFFFFF, #FCFC00 100%);
  padding: 20px 15px 15px 15px;
  position: relative;
}
#login-buttons {
  display: block;
}
h1 {
  font-size: 1.5em;
  margin: 0;
  margin-bottom: 10px;
  display: inline-block;
  margin-right: 1em;
}
form {
  margin-top: 10px;
  margin-bottom: -10px;
  position: relative;
}
.new-task input {
  box-sizing: border-box;
  padding: 10px 0;
  background: transparent;
  border: none;
  width: 100%;
  padding-right: 80px;
  font-size: 1em;
} 
.new-task input:focus{
  outline: 0;
}
ul {
  margin: 0;
  padding: 0;
  background: white;
}
.delete {
  float: right;
  font-weight: bold;
  background: none;
  font-size: 1em;
  border: none;
  position: relative;
}
li {
  position: relative;
  list-style: none;
  padding: 15px;
  border-bottom: #eee solid 1px;
}
li .text {
  margin-left: 10px;
} 
li.checked {
  color: #888;
}
li.checked .text {
  text-decoration: line-through;
} 
li.private {
  background: #eee;
  border-color: #ddd;
}
header .hide-completed {
  float: right;
}
.toggle-private {
  margin-left: 5px;
}
@media (max-width: 600px) {
  li {
    padding: 12px 15px;
  }
  .search {
    width: 150px;
    clear: both;
  }
  .new-task input {
    padding-bottom: 5px;
  }
}
</code></pre>
<p>Außerdem fügen wir das Logo ein, dafür erstellen wir im Root-Verzeichnis einen neuen Ordner “public” und legen das Logo darin ab.</p>
<p>In der Datei <code>body.html</code>(“imports\ui”) fügen wir nun im Header das Logo ein:</p>
<pre><code>&lt;img style="display: block; text-align: center;" src="/logodogs.png" width="100%" border="0" alt="Rubidogs ToDo"&gt;
</code></pre>
<h4 id="mongodb">MongoDB</h4>
<p>Es wird im “imports” Ordner ein Unterordner “api” erstellt und in diesem die Datei <code>tasks.js</code> mit folgendem Inhalt:</p>
<pre><code>import { Mongo } from 'meteor/mongo';
export const Tasks = new Mongo.Collection('tasks');
</code></pre>
<p>In der <code>main.js</code> aus dem Server-Ordner (server/main.js) ergänzen wir anschließend folgenden Code:</p>
<pre><code>import '../imports/api/tasks.js';
</code></pre>
<p>Somit wird nun die MongoDB Collection für unsere Taskliste erzeugt.<br>
Im clientseitigen Teil laden wir die Tasks nun aus der Collection, indem wir unter “imports\ui” im File <code>body.js</code> folgende Änderungen vornehmen:<br>
Vorher:</p>
<pre><code>import { Template } from 'meteor/templating';
import './body.html';
Template.body.helpers({
  tasks: [
    { text: 'This is task 1' },
    { text: 'This is task 2' },
    { text: 'This is task 3' },
  ],
});
</code></pre>
<p>Wir fügen den Import der tasts hinzu, und ersetzen den Aufruf dieser, sodass diese aus der Collection geladen werden.<br>
Nachher:</p>
<pre><code>import { Template } from 'meteor/templating';
import { Tasks } from '../api/tasks.js';
import './body.html';
 
Template.body.helpers({
    tasks() {
        return Tasks.find({});
      },
});
</code></pre>
<p>Die bisher erfassten Tasks verschwinden nun von unserer Seite.</p>
<h4 id="tasks-erfassen">Tasks erfassen</h4>
<p>In einer zweiten Shell öffnen wir die MongoDB, nachdem wir wieder in den Meteor-ToDo-Ordner navigiert haben:</p>
<pre><code>cd ..
cd ..
cd simple-todos
meteor mongo
</code></pre>
<p>Dies sollte wie folgt aussehen:<br>
<img src="https://i.ibb.co/Cn5N74j/meteor-mongo.png" alt="enter image description here"></p>
<p>Nun legen wir die ersten Tasks an:</p>
<pre><code>db.tasks.insert({ text: "Feed the dog!", createdAt: new  Date() });
db.tasks.insert({ text: "Go for a walk", createdAt: new  Date() });
db.tasks.insert({ text: "Get a puppy", createdAt: new  Date() });
db.tasks.insert({ text: "Feed the cat!", createdAt: new  Date() });
db.tasks.insert({ text: "Go for another walk", createdAt: new  Date() });
</code></pre>
<p>Da wir aber künftig auch Tasks über die Applikation anlegen wollen, brauchen wir hierzu eine Formular, dieses fügen wir ein, indem wir in der (“imports\ui”) <code>body.html</code>" folgenden Code unter der Überschrift “Rubidogs Todos” ergänzen. Unser "<code>&lt;header&gt;</code>-Element sieht also nun so aus:</p>
<pre><code> &lt;header&gt;
	&lt;img style="display: block; text-align: center;" src="/logodogs.png" width="100%" border="0" alt="Rubidogs ToDo"&gt;
    &lt;h1&gt;Todo List&lt;/h1&gt;
	&lt;form class="new-task"&gt;
       &lt;input type="text" name="text" placeholder="Type to add new tasks" /&gt;
    &lt;/form&gt;
&lt;/header&gt;
</code></pre>
<p>Damit die Eingaben auch verarbeitet werden muss ein Handler implementiert werden, dies geschieht in der “imports\ui” <code>body.js</code> durch das ergänzen den anschließenden Codes am Ende vom File:</p>
<pre><code>Template.body.events({
    'submit .new-task'(event) {
      // Prevent default browser form submit
      event.preventDefault();
  
      // Get value from form element
      const target = event.target;
      const text = target.text.value;
  
      // Insert a task into the collection
      Tasks.insert({
        text,
        createdAt: new Date(), // current time
      });
  
      // Clear form
      target.text.value = '';
    },
  });
</code></pre>
<p>Nun können wir über die UI bereits Tasks hinzufügen.<br>
Diese sortieren wir nach Erstelldatum mit folgender Anpassung in der “imports/ui” <code>body.js</code> :</p>
<pre><code>return Tasks.find([]);
</code></pre>
<p>wird angepasst zu:</p>
<pre><code>  return Tasks.find({}, { sort: { createdAt: -1 } });
</code></pre>
<h4 id="tasks-bearbeiten">Tasks bearbeiten</h4>
<p>Um auch wirklich mit den Aufgaben arbeiten zu können, erstellen wir im Folder “imports\ui” das File <code>tasks.html</code> und füllen dies mit einem template:</p>
<pre><code>&lt;template name="task"&gt;
    &lt;li class="{{#if checked}}checked{{/if}}"&gt;
      &lt;button class="delete"&gt;&amp;times;&lt;/button&gt;
      &lt;input type="checkbox" checked="{{checked}}" class="toggle-checked" /&gt;
      &lt;span class="text"&gt;{{text}}&lt;/span&gt;
    &lt;/li&gt;
  &lt;/template&gt;
</code></pre>
<p>Im File <code>body.html</code>entfernen wir das bisher genutzte Task-Template (löschen also folgenden Code heraus):</p>
<pre><code> &lt;template name="task"&gt;
    &lt;li&gt;{{text}}&lt;/li&gt;
 &lt;/template&gt;
</code></pre>
<p>Nun erstellen wir im “imports\ui” Ordner das File <code>tasks.js</code>und befüllen es wie folgt:</p>
<pre><code>import { Template } from 'meteor/templating';
import { Tasks } from '../api/tasks.js';
import './tasks.html';
 
Template.task.events({
  'click .toggle-checked'() {
    // Set the checked property to the opposite of its current value
    Tasks.update(this._id, {
      $set: { checked: ! this.checked },
    });
  },
  'click .delete'() {
    Tasks.remove(this._id);
  },
});
</code></pre>
<p>Somit haben wir unserer Taskliste die ersten Event-Handler hinzugefügt mit denen gearbeitet werden kann.<br>
<img src="https://i.ibb.co/84djj8K/meteor-working.png" alt="enter image description here"></p>
<p>Um erledigte Aufgaben auszublenden und diese nicht nach dem Erledigen löschen zu müssen, fügen wir in der <code>body.html</code>im “imports\ui” Ordner ein neues Label ein:</p>
<pre><code>&lt;label class="hide-completed"&gt;
    &lt;input type="checkbox" /&gt;
    Hide Completed Tasks
&lt;/label&gt;
</code></pre>
<p>Anschließend muss</p>
<pre><code>meteor add reactive-dict
</code></pre>
<p>in der zweiten Shell (die wir für MongoDB genutzt haben) ausgeführt werden und die <code>body.js</code>im “imports\ui” Ordner angepasst werden.<br>
Es muss das reactive-dict importiert werden und ein neues Template erstellt werden:</p>
<pre><code>import { ReactiveDict } from 'meteor/reactive-dict';

Template.body.onCreated(function bodyOnCreated() {
this.state = new ReactiveDict();
  });
</code></pre>
<p>Außerdem benötigen wir einen Handler für die Checkbox:</p>
<pre><code>  'change .hide-completed input'(event, instance) {
        instance.state.set('hideCompleted', event.target.checked); },
</code></pre>
<p>und müssen die Tasks herausfiltern, die bereits abgeschlossen sind:</p>
<pre><code>const instance = Template.instance();
        if (instance.state.get('hideCompleted')) {
          // If hide completed is checked, filter tasks
          return Tasks.find({ checked: { $ne: true } }, { sort: { createdAt: -1 } });
}
 // Otherwise, return all of the tasks
</code></pre>
<p>Nach diesen Änderungen schaut unser <code>body.js</code>File wie folgt aus:</p>
<pre><code>import { Template } from 'meteor/templating';
import { Tasks } from '../api/tasks.js';
import { ReactiveDict } from 'meteor/reactive-dict';
import './tasks.js';
import './body.html';

Template.body.onCreated(function bodyOnCreated() {
    this.state = new ReactiveDict();
  });

Template.body.helpers({
    tasks() {
		const instance = Template.instance();
        if (instance.state.get('hideCompleted')) {
          // If hide completed is checked, filter tasks
          return Tasks.find({ checked: { $ne: true } }, { sort: { createdAt: -1 } });
        }
        // Otherwise, return all of the tasks
   return Tasks.find({}, { sort: { createdAt: -1 } });
      },
});

 
Template.body.events({
    'submit .new-task'(event) {
      // Prevent default browser form submit
      event.preventDefault();
  
      // Get value from form element
      const target = event.target;
      const text = target.text.value;
  
      // Insert a task into the collection
      Tasks.insert({
        text,
        createdAt: new Date(), // current time
      });
  
      // Clear form
      target.text.value = '';
    },
	    'change .hide-completed input'(event, instance) {
        instance.state.set('hideCompleted', event.target.checked);
      },
  });
</code></pre>
<p>Um nun noch eine Anzahl, der unabgeschlossenen Tasks anzeigen zu lassen, passen wir sowohl <code>body.js</code> als auch <code>body.html</code> im “imports\ui” Ordner geringfügig an:</p>
<h5 id="body.js-1">body.js</h5>
<pre><code>incompleteCount() {
return Tasks.find({ checked: { $ne: true } }).count();
</code></pre>
<p>Dies wird am Ende des <code>Template.body.helpers</code>eingefügt.</p>
<h5 id="vorher">Vorher</h5>
<pre><code>Template.body.helpers({
    tasks() {
		const instance = Template.instance();
        if (instance.state.get('hideCompleted')) {
          // If hide completed is checked, filter tasks
          return Tasks.find({ checked: { $ne: true } }, { sort: { createdAt: -1 } });
        }
        // Otherwise, return all of the tasks
   return Tasks.find({}, { sort: { createdAt: -1 } });
      },
	  
});
</code></pre>
<h5 id="nachher">Nachher</h5>
<pre><code>Template.body.helpers({
    tasks() {
		const instance = Template.instance();
        if (instance.state.get('hideCompleted')) {
          // If hide completed is checked, filter tasks
          return Tasks.find({ checked: { $ne: true } }, { sort: { createdAt: -1 } });
        }
        // Otherwise, return all of the tasks
   return Tasks.find({}, { sort: { createdAt: -1 } });
      },
	      incompleteCount() {
        return Tasks.find({ checked: { $ne: true } }).count();}
});
</code></pre>
<h5 id="body.html-1">body.html</h5>
<p>Im <code>&lt;header&gt;</code>-Element fügen wir den Counter ein:</p>
<pre><code>&lt;h1&gt;Rubidogs Todos ({{incompleteCount}})&lt;/h1&gt;
</code></pre>
<h3 id="user-accounts">User Accounts</h3>
<p>Damit auch zielführend gearbeitet werden kann, sollte nicht jeder User alle Tasks sehen, hierfür bedarf es User Accounts.<br>
Mittels</p>
<pre><code>meteor add accounts-ui accounts-password
</code></pre>
<p>aktivieren wir das Meteor-Account System (ausgeführt aus der zweiten Shell) und bekommen in der ersten Shell (in der Meteor ausgeführt wird) folgende Meldung:<br>
<img src="https://i.ibb.co/3yYRLdD/meteor-slow.png" alt="enter image description here"><br>
und installieren befolgen die Hinweise daraus in der zweiten Shell:</p>
<pre><code>meteor npm install -save bcrypt
</code></pre>
<p>In unserem <code>&lt;body.html&gt;</code>im “imports\ui” Ordner  fügen wir den Login-Button direkt unter der Checkbox zum Ausblenden abgeschlossener Tasks ein:</p>
<pre><code>{{&gt; loginButtons}}
</code></pre>
<p>Außerdem müssen wir einen neuen “startup” Ordner anlegen (imports\startup) und darin ein <code>accounts-config.js</code>file, zur Konfiguration:</p>
<pre><code>import { Accounts } from 'meteor/accounts-base';
Accounts.ui.config({
  passwordSignupFields: 'USERNAME_ONLY',
});
</code></pre>
<p>Dies müssen wir noch in unser <code>main.js</code>übernehmen (client\main.js):</p>
<pre><code>import '../imports/startup/accounts-config.js';
</code></pre>
<p>Um den User-Accounts eine Daseinsberechtigung zu geben, fügen wir den Tasks eine UserId und den Usernamen hinzu, um diese Eigenschaften für Zuweisungen nutzen zu können, hierzu modifzieren wir <code>body.js</code>(imports\ui):</p>
<pre><code>import { Meteor } from 'meteor/meteor';
...
Tasks.insert({
    text,
    createdAt: new Date(), // current time
    owner: Meteor.userId(),
    username: Meteor.user().username,
  });
</code></pre>
<p>und blenden sogleich nur dann die Eingabemaske zum Anlegen von Aufgaben ein, wenn der Benutzer eingeloggt ist. Hierzu fügen wir einen if-Block in das<code>body.html</code> (imports\ui) File ein, direkt unter dem Login-Button:</p>
<pre><code>  {{#if currentUser}}
    &lt;form class="new-task"&gt;
        &lt;input type="text" name="text" placeholder="Type to add new tasks" /&gt;
    &lt;/form&gt;
  {{/if}}
</code></pre>
<p>Im File <code>tasks.html</code>(import\ui) editieren wir die Anzeige der Tasks:</p>
<pre><code>&lt;span class="text"&gt;{{text}} - &lt;strong&gt;{{username}}&lt;/strong&gt;&lt;/span&gt;
</code></pre>
<h4 id="security">Security</h4>
<p>Da es in jedem neu erstellten Meteor-Projekt ersteinmal möglich ist, dass man clientseitig Änderungen an der Datenbank durchführt, entfernen wir dieses Package nun via Powershell:</p>
<pre><code>meteor remove insecure
</code></pre>
<p>Im Folder “imports/api” ersetzen wir den Inhalt des <code>tasks.js</code>Files mit folgendem Code, wodurch uns eine bessere Verwendung der dort definierten Methoden ermöglicht wird:</p>
<pre><code>import { Meteor } from 'meteor/meteor';
import { Mongo } from 'meteor/mongo';
import { check } from 'meteor/check';
export const Tasks = new Mongo.Collection('tasks');
Meteor.methods({
  'tasks.insert'(text) {
    check(text, String);
    // Make sure the user is logged in before inserting a task
    if (! this.userId) {
      throw new Meteor.Error('not-authorized');
    }
    Tasks.insert({
      text,
      createdAt: new Date(),
      owner: this.userId,
      username: Meteor.users.findOne(this.userId).username,
    });
  },
  'tasks.remove'(taskId) {
    check(taskId, String);
    Tasks.remove(taskId);
  },
  'tasks.setChecked'(taskId, setChecked) {
    check(taskId, String);
    check(setChecked, Boolean);
    Tasks.update(taskId, { $set: { checked: setChecked } });
  },
});
</code></pre>
<p>Welche wir im <code>body.js</code> File (“imports\ui”) sogleich verwenden werden und unseren Insert-Aufruf anpassen:</p>
<pre><code>   // Insert a task into the collection
  Meteor.call('tasks.insert', text);
</code></pre>
<p>Im File <code>tasks.js</code>(“imports\ui”) löschen wir den nicht mehr benötigten Import der Tasks und ersetzen ebenfalls die Methoden durch die neuen:</p>
<pre><code>import { Meteor } from 'meteor/meteor';
import { Template } from 'meteor/templating';
import './tasks.html';
  Template.task.events({
      'click .toggle-checked'() {
        // Set the checked property to the opposite of its current value
        Meteor.call('tasks.setChecked', this._id, !this.checked);
      },
      'click .delete'() {
        Meteor.call('tasks.remove', this._id);
      },
    });
</code></pre>
<p><strong>Nun können wir uns sicher sein, dass nur eingeloggte User Tasks erstellen können.</strong></p>
<h4 id="privacy">Privacy</h4>
<p>Um Aufgaben nur für bestimmte Benutzer sichtbar zu machen, müssen wir die autopublish-Funktion, mit der alle neuen Meteor-Apps erstellt werden, entfernen und über die Funktionen Meteor.publish und Meteor.subscribe gezielt steuern, wann der Server was zum Client schickt.<br>
Wir entfernen das autopublish-Package mit Powershell aus unserem App-Verzeichnis:</p>
<pre><code>meteor remove autopublish
</code></pre>
<p>Wodurch beim nächsten Refresh der Applikation, die Liste der Aufgaben leer bleibt.<br>
In der API (“imports\api”), genauer im File <code>tasks.js</code> fügen wir nun eine IF-Bedingung ein, die, wenn sie vom Server aufgerufen wird, alle Tasks “published”. Dazu fügen wir folgenden Code, direkt nach der <code>export const Tasks</code>-Zeile ein:</p>
<pre><code>if (Meteor.isServer) {
    // This code only runs on the server
    Meteor.publish('tasks', function tasksPublication() {
      return Tasks.find();
    });
}
</code></pre>
<p>Außerdem passen wir die Erstellung des Body-Templates an, sodass hier die Publication aufgerufen wird (“imports\ui”) <code>body.js</code>:</p>
<pre><code>Template.body.onCreated(function bodyOnCreated() {
    this.state = new ReactiveDict();
	Meteor.subscribe('tasks');
  });
</code></pre>
<h4 id="private-aufgaben">Private Aufgaben</h4>
<p>Wir erstellen eine neue Eigenschaft, die es uns ermöglichen wird, private Aufgaben zu filtern und einen Button, der es uns ermöglicht solche zu erstellen, indem wir im File <code>task.html</code>(“imports\ui”) folgende Zeilen einfügen (direkt unter der Checkbox):</p>
<pre><code>{{#if isOwner}}
  &lt;button class="toggle-private"&gt;
    {{#if private}}
      Private
    {{else}}
      Public
    {{/if}}
  &lt;/button&gt;
{{/if}}
</code></pre>
<p>und am Anfang dieses Files die class bearbeiten und abändern auf:</p>
<pre><code>&lt;li class="{{#if checked}}checked{{/if}} {{#if private}}private{{/if}}"&gt;
</code></pre>
<p>Das Script für die Tasks müssen wir ebenfalls anpassen, hierzu wird im File <code>tasks.js</code>(“imports\ui”) unter den Importen folgender Code ergänzt:</p>
<pre><code>  Template.task.helpers({
      isOwner() {
	      return this.owner === Meteor.userId();
		      },
 });
</code></pre>
<p>und fügen einen Event-Handler hinzu (<code>click. delete</code> war bereits vorhanden):</p>
<pre><code> 'click .delete'() {
Meteor.call('tasks.remove', this._id);
},
'click .toggle-private'() {
    Meteor.call('tasks.setPrivate', this._id, !this.private);
  },
</code></pre>
<p>Im taskzugehörigen API-File <code>tasks.js</code>(“imports\api”) definieren wir die <code>setPrivate</code>-Methode:</p>
<pre><code>Tasks.update(taskId, { $set: { checked: setChecked } });
},
'tasks.setPrivate'(taskId, setToPrivate) {
    check(taskId, String);
    check(setToPrivate, Boolean);
    const task = Tasks.findOne(taskId);
    // Make sure only the task owner can make a task private
    if (task.owner !== this.userId) {
      throw new Meteor.Error('not-authorized');
    }
    Tasks.update(taskId, { $set: { private: setToPrivate } });
  },
</code></pre>
<p>und passen unsere Einschränkung bezüglich der Publikation an:</p>
<pre><code>if (Meteor.isServer) {
// This code only runs on the server
// Only publish tasks that are public or belong to the current user
Meteor.publish('tasks', function tasksPublication() {
  return Tasks.find({
    $or: [
      { private: { $ne: true } },
      { owner: this.userId },
    ],
  });
});
</code></pre>
<p>}</p>
<p>Abschließend verbessern wir die Methoden <code>deleteTask</code>und <code>setChecked</code>im <code>tasks.js</code>File (“imports\api”) indem wir eine Überprüfung auf die UserId einfügen:</p>
<pre><code>'tasks.remove'(taskId) {
    check(taskId, String);
    const task = Tasks.findOne(taskId);
    if (task.owner !== this.userId) {
      //make sure only the owner can delete it
      throw new Meteor.Error('not-authorized');
    }
    Tasks.remove(taskId);
  },
  'tasks.setChecked'(taskId, setChecked) {
    check(taskId, String);
    check(setChecked, Boolean);
    const task = Tasks.findOne(taskId);
    if (task.private &amp;&amp; task.owner !== this.userId) {
       // If the task is private, make sure only the owner can check it off
      throw new Meteor.Error('not-authorized');
    }
</code></pre>
<p><strong>Mit diesem Schritt ist die Standard-Installation der Meteor-ToDo App abgeschlossen.</strong></p>
<h2 id="deployment-in-einer-heroku.com---instanz">Deployment in einer <a href="http://heroku.com">heroku.com</a> - Instanz</h2>
<h3 id="erstellen-eines-heroku-accounts">Erstellen eines heroku-Accounts</h3>
<p>Auf <a href="http://www.heroku.com">www.heroku.com</a> rechts oben auf Sign up klicken und einen kostenlosen Account erstellen: <img src="https://i.ibb.co/rbsj2td/herokusignup.png" alt="enter image description here"></p>
<p>Nachdem die E-Mail-Adresse bestätigt wurde, wird das Kennwort festgelegt und man wird zum Dashboard weitergeleitet.<br>
Dort klicken wir unten auf den Link zum “Heroku Dev Center” und suchen in diesem nach “Heroku CLI”, öffnen den ersten Treffer und laden die Heroku CLI dort herunter (in diesem Tutorial Windows 64 Bit).<br>
Der Standardinstallationspfad ist: <code>C:\Program Files\heroku</code>.<br>
In diesem Pfad öffnen wir die Powershell und stellen mit dem Befehl</p>
<pre><code>heroku login
</code></pre>
<p>eine Verbindung zu heroku her, diese wird im Browser bestätigt.<br>
Nun erstellen wir eine neue App:</p>
<pre><code>heroku apps:create &lt;nameEurerApp&gt;
</code></pre>
<p>und aktivieren ein buildpack für das Deplyoment:</p>
<pre><code>heroku buildpacks:set admithub/meteor-horse
</code></pre>
<blockquote>
<p><em>In einem ersten Durchlauf schlug die buildpack-configuration fehl, bis die Applikation zum ersten Mal (falsch) deployed war. Im zweiten Durchlauf funktionierte dies ohne Probleme.</em></p>
</blockquote>
<h3 id="konfiguration">Konfiguration</h3>
<p>Mittels dem Befehl</p>
<pre><code>heroku addons:create mongolab:sandbox
</code></pre>
<p>soll eine Mongolab (MongoDB) Instanz im Free Tier angelegt werden, dies funktionierte leider nur, nachdem unter Account Settings eine Kreditkarte hinterlegt wurde, selbst wenn keine Kosten entstehen.<br>
Alternativ kann man die MongoDB bei Mongolab manuell aufsetzen. Hierzu auf <a href="http://mlab.com">mlab.com</a> navigieren und dort registrieren (man wird zu <a href="http://mongodb.com">mongodb.com</a> weitergeleitet und errichtet dort einen kostenlosen MongoDB Atlas Account).<br>
Dort erstellen wir einen neuen Cluster auf einem Azure Server in Westeuropa im Free Tier und warten die Erstellung ab.<br>
Anschließend wird die Connection eingerichtet, hierzu erlauben wir “Access von Anywhere” und klicken anschließend auf “Connect your Application” und wählen die gewünschte Serversprache aus (Node.js) .<br>
<img src="https://i.ibb.co/rMrJBtT/mongoconnect.png" alt="enter image description here"><br>
Den Connectionstring kopieren wir uns in einen Texteditor</p>
<p>Anschließend wird der String angepasst:</p>
<h5 id="vorher-1">Vorher</h5>
<pre><code>mongodb+srv://JanKrieger:&lt;password&gt;@testcluster-aresu.azure.mongodb.net/&lt;dbname&gt;?retryWrites=true&amp;w=majority
</code></pre>
<h5 id="nachher-1">Nachher</h5>
<pre><code>mongodb://JanKrieger:&lt;password&gt;@testcluster-aresu.azure.mongodb.net/&lt;dbname&gt;
</code></pre>
<p>Nun fügen wir die MongoLab App hinzu</p>
<pre><code>heroku addons:create mongolab
</code></pre>
<p>und fügen wir mittels Heroku CLI unserer Applikation als Datenbank-Pfad ein:</p>
<pre><code>heroku config:add MONGODB_URI: mongodb://JanKrieger:&lt;password&gt;@testcluster-aresu.azure.mongodb.net/&lt;dbname&gt;
</code></pre>
<p>Außerdem fügen wir gleich die ROOT-URL zur App hinzu:</p>
<pre><code>heroku config:add ROOT_URL=https://&lt;nameofyourapp&gt;.herokuapp.com
</code></pre>
<p>Ein Abruf der Configuration sollte ähnlich aussehen (je nach gewählter Variante zur Erstellung der MongoDB):</p>
<pre><code>heroku config
</code></pre>
<p><img src="https://i.ibb.co/P9PKP86/heroku-config.png" alt="enter image description here"></p>
<p>Im Anschluss überprüfen wir unseren Remote-Branch, damit wir auch korrekt zu heroku pushen:</p>
<pre><code>git remote -v
</code></pre>
<p>Dies sollte einen Output liefern, ähnlich dem folgenden:<br>
<img src="https://i.ibb.co/Ch4FvJG/heroku-CLI-gitremote.png" alt="enter image description here"></p>
<h3 id="deployment">Deployment</h3>
<p>Mittels einem git push zum heroku master branch laden wir anschließend unsere Applikation hoch, das installierte buildpack übernimmt dann die Aufgabe der korrekten Erstellung des Builds.</p>
<pre><code>git commit -am "deploy to heroku"
git push heroku master 
</code></pre>
<p>Den Durchlauf des Builds können wir nun in der Powershell verfolgen oder in unserer Heroku-App unter “Activity” nachträglich ansehen:<br>
<img src="https://i.ibb.co/6nCdhzs/heroku-deployed.png" alt="enter image description here"></p>
<p>Sollte dies erfolgreich verlaufen, können wir nun versuchen unsere App über <code>https://&lt;appname&gt;.herokuapp.com</code>aufrufen:<br>
<img src="https://i.ibb.co/ysDBCmH/success.png" alt="enter image description here"></p>
<h2 id="zusatz-facebook-login">Zusatz: Facebook Login</h2>
<p>Wir installieren per Powershell die Packages für die Facebook-Authentifizierung und die Konfigurations-UI:</p>
<pre><code>meteor add accounts-facebook
meteor add facebook-config-ui
</code></pre>
<p>commiten und pushen den code wieder auf den Server:</p>
<pre><code>git commit -am "fb login"
git push heroku master
</code></pre>
<p>Während der Build läuft besuchen wir die Seite <a href="https://developers.facebook.com/">https://developers.facebook.com/</a> und erstellen eine neue App:<br>
<img src="https://i.ibb.co/KWTs0fw/FBCreate.png" alt="enter image description here"><br>
Sobald diese erstellt ist, öffnen wir die Einstellungen &gt; Allgemeines und notieren App-ID und App-Geheimcode und tragen eine URL zur Datenrichtlinie und zur Nutzungsbedingung ein.<br>
<img src="https://i.ibb.co/w7Djmzd/fbsettings.png" alt="enter image description here"><br>
Hinweis: In diesem Studentenprojekt wurde keine Page für die Datenrichtlinie und die Nutzungsbedingungen erstellt, dies ist für eine produktive Nutzung jedoch unerlässlich!</p>
<p>Nach einem Klick auf “Produkte +” im Menü auf der linken Seite der Page, wählen wir den Facebook Login aus und klicken auf einrichten und dann auf “WWW”, geben im nachfolgenden Dialog die URL unserer Website ein<br>
( <a href="https://jk-simple-todos.herokuapp.com">https://jk-simple-todos.herokuapp.com</a> ) und öffnen die erweiterten Einstellungen. Dort tragen wir unter “Gültige OAuth Redirect URIs” den URL unserer Website ein und erweitern diese um<br>
<code>/_oauth/facebook</code>.<br>
<img src="https://i.ibb.co/0VzFgx2/fbloginsetting.png" alt="enter image description here"><br>
Wir speichern die Einstellungen und schieben den Regler im oberen Berech der Seite von “In Entwicklung” auf “Live”.</p>
<p>In unserer App erscheint nach erfolgreichem Build nun beim Klick auf “SignIn” ein “Configure Facebook Login” Button, welchen wir anklicken.<br>
Dort tragen wir lediglich App ID und App Secret ein und bestätigen die Einstellungen.<br>
<img src="https://i.ibb.co/rmBppZN/meteor-fb.png" alt="enter image description here"></p>
<p>Nun können wir uns per Facebook in unserer Meteor-Todo-App anmelden:<br>
<img src="https://i.ibb.co/X2ZCMZn/FB-Login.png" alt="enter image description here"><br>
Die Anzeige des Usernamens neben dem Task bei Facebook-Anmeldung wurde leider in der Frist nicht mehr umgesetzt.</p>
<p>Edit 17.06.2020:<br>
Fehler bei der manuellen Verbindung der MongoDB ausgebessert (Connect from anywhere)</p>
<p>Anmerkung:<br>
Ursprünglich war eine Bereitstellung auf Azure geplant, diese wurde nach Problemen mit dem Tool “Demeteorizer” jedoch abgebrochen und anstelle dessen wurde die Bereitstellung über heroku durchgeführt. Daher war der Azure App Service ohne Verwendung und die Dokumentation konnte hier seinen Platz finden.</p>

