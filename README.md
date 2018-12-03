<!DOCTYPE html>
<h1 id="firstHeading" class="firstHeading" lang="ru"> SQLAlchemy</h1>			<div id="bodyContent" class="mw-body-content">
				<div id="mw-content-text" lang="ru" dir="ltr" class="mw-content-ltr"><div class="mw-parser-output"><div id="toc" class="toc"><input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none" /><div for="toctogglecheckbox"></label></span></div>
<ul>

<h2><span id=".D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2_SQLAlchemy"></span><span class="mw-headline" id="Введение_в_SQLAlchemy">Введение в SQLAlchemy
<table class="metadata plainlinks ambox ambox-delete">
<tbody><tr>
</td>

<td class="widthhack">
</td></tr></tbody></table>
<p><a href="http://ru.wikipedia.nym.su/wiki/SQLAlchemy" class="extiw" title="w:SQLAlchemy">SQLAlchemy</a>&#160;— это программное обеспечение с открытым исходным кодом для работы с базами данных при помощи языка SQL. Оно реализует технологию программирования <a href="http://ru.wikipedia.nym.su/wiki/ORM" class="extiw" title="w:ORM">ORM</a> (Object-Relational Mapping), которая связывает базы данных с концепциями объектно-ориентированных языков программирования. SQLAlchemy позволяет описывать структуры баз данных и способы взаимодействия с ними прямо на языке <a href="/wiki/Python" title="Python">Python</a>.
</p><p>SQLAlchemy была выпущена в феврале 2006 и быстро стала одним из самых распространенных инструментов ORM среди разработчиков на Python.
SQLAlchemy обладает несколькими областями применения, которые могут использоваться как вместе, так и по отдельности. 
</p>
<h2><span id=".D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_SQLAlchemy"></span><span class="mw-headline" id="Установка_SQLAlchemy">Установка SQLAlchemy</span><span class="mw-editsection"></h2>
<p>Вы можете установить SQLAlchemy с нуля, для этого можете просто набрать в консоли:
</p>pip3 install sqlalchemy
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="c1"></span>
</pre></div>
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="c1"></span>
</pre></div>
<p>Для проверки правильности установки следует проверить версию библиотеки:
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="kn">import</span> <span class="nn">sqlalchemy</span><span class="c1"> #начните работу с этой библиотеки</span>
<span class="k">print</span> <span class="s2">&quot;Версия SQLAlchemy:&quot;</span><span class="p">,</span> <span class="n">sqlalchemy</span><span class="o">.</span><span class="n">__version__</span><span class="c1"> #посмотреть версию SQLALchemy</span>
</pre></div>
<h2><span id=".D0.9E.D0.B1.D1.8A.D0.B5.D0.BA.D1.82.D0.BD.D0.BE-.D1.80.D0.B5.D0.BB.D1.8F.D1.86.D0.B8.D0.BE.D0.BD.D0.BD.D0.B0.D1.8F_.D0.BC.D0.BE.D0.B4.D0.B5.D0.BB.D1.8C_SQLAlchemy"></span><span class="mw-headline" id="Объектно-реляционная_модель_SQLAlchemy">Объектно-реляционная модель SQLAlchemy</span><span class="mw-editsection"><span class="mw-editsection-bracket">
<h5><span id=".D0.A1.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81_.D0.B1.D0.B0.D0.B7.D0.BE.D0.B9_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85"></span><span class="mw-headline" id="Соединение_с_базой_данных">Соединение с базой данных.</span><span class="mw-editsection">
<p>В этом уроке мы будем использовать только БД <i>SQLite</i>, хранящуюся в памяти.
Чтобы соединиться с СУБД, мы используем функцию <i>create_engine()</i>:
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="kn">from</span> <span class="nn">sqlalchemy</span> <span class="kn">import</span> <span class="n">create_engine</span>
<span class="n">engine</span> <span class="o">=</span> <span class="n">create_engine</span><span class="p">(</span><span class="s1">&#39;sqlite:///:memory:&#39;</span><span class="p">,</span> <span class="n">echo</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
</pre></div>
<h5><span id=".D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.82.D0.B0.D0.B1.D0.BB.D0.B8.D1.86.D1.8B_.D0.B2_.D0.B1.D0.B0.D0.B7.D0.B5_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85"></span><span class="mw-headline" id="Создание_таблицы_в_базе_данных">Создание таблицы в базе данных.
<p>Далее мы пожелаем рассказать SQLAlchemy о наших таблицах. Мы начнем с одиночной таблицы <i>users</i>, В которой будем хранить записи о наших конечных пользователях, которые посещают некий сайт N. Мы определим нашу таблицу внутри каталога <i>MetaData</i>, используя конструктор <i>Table()</i>.
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="kn">from</span> <span class="nn">sqlalchemy</span> <span class="kn">import</span> <span class="n">Table</span><span class="p">,</span> <span class="n">Column</span><span class="p">,</span> <span class="n">Integer</span><span class="p">,</span> <span class="n">String</span><span class="p">,</span> <span class="n">MetaData</span><span class="p">,</span> <span class="n">ForeignKey</span>
<span class="n">metadata</span> <span class="o">=</span> <span class="n">MetaData</span><span class="p">()</span>
<span class="n">users_table</span> <span class="o">=</span> <span class="n">Table</span><span class="p">(</span><span class="s1">&#39;users&#39;</span><span class="p">,</span> <span class="n">metadata</span><span class="p">,</span>
    <span class="n">Column</span><span class="p">(</span><span class="s1">&#39;id&#39;</span><span class="p">,</span> <span class="n">Integer</span><span class="p">,</span> <span class="n">primary_key</span><span class="o">=</span><span class="bp">True</span><span class="p">),</span>
    <span class="n">Column</span><span class="p">(</span><span class="s1">&#39;name&#39;</span><span class="p">,</span> <span class="n">String</span><span class="p">),</span>
    <span class="n">Column</span><span class="p">(</span><span class="s1">&#39;fullname&#39;</span><span class="p">,</span> <span class="n">String</span><span class="p">),</span>
    <span class="n">Column</span><span class="p">(</span><span class="s1">&#39;password&#39;</span><span class="p">,</span> <span class="n">String</span><span class="p">)</span>
<span class="p">)</span>
</pre></div>
</p><p>Далее же мы вызовем метод <i>create_all()</i> и передадим ему наш объект <i>engine</i>, который и указывает на базу.
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="n">metadata</span><span class="o">.</span><span class="n">create_all</span><span class="p">(</span><span class="n">engine</span><span class="p">)</span>
</pre></div>
</p>
<h5><span id=".D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D1.81.D1.81.D0.B0_Python_.D0.B4.D0.BB.D1.8F_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B2_.D1.82.D0.B0.D0.B1.D0.BB.D0.B8.D1.86.D1.83"></span><span class="mw-headline" id="Определение_класса_Python_для_отображения_в_таблицу">Определение класса Python для отображения в таблицу.
</p>
<p>В то время, как класс <i>Table</i> хранит информацию о нашей БД, он ничего не говорит о логике объектов, что используются нашим приложением. SQLAlchemy считает это отдельным вопросом. Для соответствия нашей таблице users создадим элементарный класс <i>User</i>. Нужно только унаследоваться от базового питоньего класса <i>Object</i> (то есть у нас совершенно новый класс).
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="k">class</span> <span class="nc">User</span><span class="p">(</span><span class="nb">object</span><span class="p">):</span>
    <span class="k">def</span> <span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">name</span><span class="p">,</span> <span class="n">fullname</span><span class="p">,</span> <span class="n">password</span><span class="p">):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">name</span> <span class="o">=</span> <span class="n">name</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">fullname</span> <span class="o">=</span> <span class="n">fullname</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">password</span> <span class="o">=</span> <span class="n">password</span>

   <span class="k">def</span> <span class="fm">__repr__</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="k">return</span> <span class="s2">&quot;&lt;User(&#39;</span><span class="si">%s</span><span class="s2">&#39;,&#39;</span><span class="si">%s</span><span class="s2">&#39;, &#39;</span><span class="si">%s</span><span class="s2">&#39;)&gt;&quot;</span> <span class="o">%</span> <span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">name</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">fullname</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">password</span><span class="p">)</span>
</pre></div>
<p><i>__init__</i>&#160;— это конструктор, <i>__repr__</i> же вызывается при операторе <i>print</i>.
Они определены здесь для удобства. Они не обязательны и могут иметь любую форму. SQLAlchemy не вызывает <i>__init__</i> напрямую
</p>
<h5><span id=".D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F"></span><span class="mw-headline" id="Настройка_отображения">Настройка отображения.
</n>
<p>Теперь мы хотим слить в едином порыве нашу таблицу user_table и класс User. Здесь нам пригодится пакет <i>SQLAlchemy ORM</i>. Мы применим функцию <i>mapper</i>, чтобы создать отображение между <i>users_table</i> и <i>User</i>.
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="kn">from</span> <span class="nn">sqlalchemy.orm</span> <span class="kn">import</span> <span class="n">mapper</span>
<span class="n">mapper</span><span class="p">(</span><span class="n">User</span><span class="p">,</span> <span class="n">users_table</span><span class="p">)</span> 
</pre></div>
<p>Функция <i>mapper()</i> создаст новый <i>Mapper-объект</i> и сохранит его для дальнейшего применения, ассоциирующегося с нашим классом. Теперь создадим и проверим объект типа <i>User</i>:
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="kn">from</span> <span class="nn">sqlalchemy.orm</span> <span class="kn">import</span> <span class="n">mapper</span>  <span class="c1">#достать &quot;Отобразитель&quot; из пакета с объектно-реляционной моделью</span>
<span class="k">print</span> <span class="n">mapper</span><span class="p">(</span><span class="n">User</span><span class="p">,</span> <span class="n">users_table</span><span class="p">)</span>  <span class="c1"># и отобразить. Передает класс User и нашу таблицу</span>
<span class="n">user</span> <span class="o">=</span> <span class="n">User</span><span class="p">(</span><span class="s2">&quot;Вася&quot;</span><span class="p">,</span> <span class="s2">&quot;Василий&quot;</span><span class="p">,</span> <span class="s2">&quot;qweasdzxc&quot;</span><span class="p">)</span>
<span class="k">print</span> <span class="n">user</span>  <span class="c1">#Напечатает &lt;User(&#39;Вася&#39;, &#39;Василий&#39;, &#39;qweasdzxc&#39;&gt;</span>
<span class="k">print</span> <span class="n">user</span><span class="o">.</span><span class="n">id</span>  <span class="c1">#Напечатает None</span>
</pre></div>
<p>Атрибут <i>id</i>, который не определен в <i>__init__</i>, все равно существует из-за того, что колонка <i>id</i> существует в объекте таблицы <i>users_table</i>. Стандартно <i>mapper()</i> создает атрибуты класса для всех колонок, что есть в <i>Table</i>. Эти атрибуты существуют как Python дескрипторы и определяют его функциональность. Она может быть очень богатой и включать в себе возможность отслеживать изменения и АВТОМАТИЧЕСКИ подгружать данные в базу, когда это необходимо.
Так как мы не сказали SQLAlchemy сохранить Василия в базу, его <i>id</i> выставлено на <i>None</i>. Когда позже мы сохраним его, в этом атрибуте будет храниться некое автоматически сформированное значение.
</p>
<h5><span id=".D0.94.D0.B5.D0.BA.D0.BB.D0.B0.D1.80.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.BE.D0.B5_.D1.81.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.82.D0.B0.D0.B1.D0.BB.D0.B8.D1.86.D1.8B.2C_.D0.BA.D0.BB.D0.B0.D1.81.D1.81.D0.B0_.D0.B8_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B7.D0.B0_.D0.BE.D0.B4.D0.B8.D0.BD_.D1.80.D0.B0.D0.B7"></span><span class="mw-headline" id="Декларативное_создание_таблицы,_класса_и_отображения_за_один_раз">Декларативное создание таблицы, класса и отображения за один раз
</n>
<p>Предыдущый подход к конфигурированию, включающий таблицу <i>Table</i>, пользовательский класс и вызов <i>mapper()</i> иллюстрируют классический пример использования SQLAlchemy, в которой очень ценится разделение задач. Большое число приложений, однако, не требуют такого разделения, и для них SQLAlchemy предоставляет альтернативный, более лаконичный стиль: декларативный.
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="kn">from</span> <span class="nn">sqlalchemy</span> <span class="kn">import</span> <span class="n">Column</span><span class="p">,</span> <span class="n">Integer</span><span class="p">,</span> <span class="n">String</span>
<span class="kn">from</span> <span class="nn">sqlalchemy.ext.declarative</span> <span class="kn">import</span> <span class="n">declarative_base</span>
<span class="n">Base</span> <span class="o">=</span> <span class="n">declarative_base</span><span class="p">()</span>
<span class="k">class</span> <span class="nc">User</span><span class="p">(</span><span class="n">Base</span><span class="p">):</span>
    <span class="n">__tablename__</span> <span class="o">=</span> <span class="s1">&#39;users&#39;</span>
    <span class="nb">id</span> <span class="o">=</span> <span class="n">Column</span><span class="p">(</span><span class="n">Integer</span><span class="p">,</span> <span class="n">primary_key</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
    <span class="n">name</span> <span class="o">=</span> <span class="n">Column</span><span class="p">(</span><span class="n">String</span><span class="p">)</span>
    <span class="n">fullname</span> <span class="o">=</span> <span class="n">Column</span><span class="p">(</span><span class="n">String</span><span class="p">)</span>
    <span class="n">password</span> <span class="o">=</span> <span class="n">Column</span><span class="p">(</span><span class="n">String</span><span class="p">)</span>
    
   <span class="k">def</span> <span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">name</span><span class="p">,</span> <span class="n">fullname</span><span class="p">,</span> <span class="n">password</span><span class="p">):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">name</span> <span class="o">=</span> <span class="n">name</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">fullname</span> <span class="o">=</span> <span class="n">fullname</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">password</span> <span class="o">=</span> <span class="n">password</span>
    <span class="k">def</span> <span class="fm">__repr__</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="k">return</span> <span class="s2">&quot;&lt;User(&#39;</span><span class="si">%s</span><span class="s2">&#39;,&#39;</span><span class="si">%s</span><span class="s2">&#39;, &#39;</span><span class="si">%s</span><span class="s2">&#39;)&gt;&quot;</span> <span class="o">%</span> <span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">name</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">fullname</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">password</span><span class="p">)</span>

<span class="c1"># Создание таблицы</span>
<span class="n">Base</span><span class="o">.</span><span class="n">metadata</span><span class="o">.</span><span class="n">create_all</span><span class="p">(</span><span class="n">engine</span><span class="p">)</span>
</pre></div>
<p>Выше&#160;— функция <i>declarative_base()</i>, что определяет новый класс, который мы назвали <i>Base</i>, от которого будет унаследованы все наши ORM-классы. Обратите внимание: мы определили объекты Column безо всякой строки имени, так как она будет выведена из имени своего атрибута.
Низлежащий объект <i>Table</i>, что создан нашей <i>declarative_base()</i> версией <i>User</i>, доступен через атрибут <i>__table__</i>
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="n">users_table</span> <span class="o">=</span> <span class="n">User</span><span class="o">.</span><span class="n">__table__</span>
</pre></div>
<p>Имющиеся метаданные MetaData также доступны:
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="n">metadata</span> <span class="o">=</span> <span class="n">Base</span><span class="o">.</span><span class="n">metadata</span>
</pre></div>
</p>
<h5><span id=".D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.B5.D1.81.D1.81.D0.B8.D0.B8"></span><span class="mw-headline" id="Создание_сессии">Создание сессии
</p>
<p>Теперь мы готовы начать наше общение с базой данных. «Ручка» базы в нашем случае&#160;— это сессия <i>Session</i>. Когда сначала мы запускаем приложение, на том же уровне нашего <i>create_engine()</i> мы определяем класс <i>Session</i>, что служит фабрикой объектов <i>сессий</i> (<i>Session</i>).
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="kn">from</span> <span class="nn">sqlalchemy.orm</span> <span class="kn">import</span> <span class="n">sessionmaker</span>
<span class="n">Session</span> <span class="o">=</span> <span class="n">sessionmaker</span><span class="p">(</span><span class="n">bind</span><span class="o">=</span><span class="n">engine</span><span class="p">)</span>
</pre></div>
<p>Такой класс <i>Session</i> будет создавать Session-объекты, которые привязаны к нашей базе.
</p><p> Так, когда вам необходимо общение с базой, вы создаете объект класса <i>Session</i>:
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="n">session</span> <span class="o">=</span> <span class="n">Session</span><span class="p">()</span>
</pre></div>
</p>
<h5><span id=".D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.BE.D0.B2.D1.8B.D1.85_.D0.BE.D0.B1.D1.8A.D0.B5.D0.BA.D1.82.D0.BE.D0.B2"></span><span class="mw-headline" id="Добавление_новых_объектов">Добавление новых объектов</span><span class="mw-editsection"></span></span></h5>
<p>Чтобы сохранить наш User-объект, нужно добавить его к нашей сессии, вызвав <i>add()</i>:
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="n">vasiaUser</span> <span class="o">=</span> <span class="n">User</span><span class="p">(</span><span class="s2">&quot;vasia&quot;</span><span class="p">,</span> <span class="s2">&quot;Vasiliy Pypkin&quot;</span><span class="p">,</span> <span class="s2">&quot;vasia2000&quot;</span><span class="p">)</span>
<span class="n">session</span><span class="o">.</span><span class="n">add</span><span class="p">(</span><span class="n">vasiaUser</span><span class="p">)</span>
</pre></div>
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="n">ourUser</span> <span class="o">=</span> <span class="n">session</span><span class="o">.</span><span class="n">query</span><span class="p">(</span><span class="n">User</span><span class="p">)</span><span class="o">.</span><span class="n">filter_by</span><span class="p">(</span><span class="n">name</span><span class="o">=</span><span class="s2">&quot;vasia&quot;</span><span class="p">)</span><span class="o">.</span><span class="n">first</span><span class="p">()</span>
<span class="c1"># &lt;User(&#39;vasia&#39;,&#39;Vasiliy Pypkin&#39;, &#39;vasia2000&#39;)&gt;</span>
</pre></div>
<p>На самом деле сессия определила, что та запись из таблицы, что она вернула, та же самая, что и запись, что она уже представляла в своей внутренней хеш-таблице объектов. Так что мы просто получили точно тот же самый объект, который только что добавили.
</p><p>Мы можем добавить больше User-объектов, использовав <i>add_all()</i>
</p>
</pre></div>
<p>А вот тут Вася решил, что его старый пароль слишком простой, так что давайте его сменим:
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="n">vasiaUser</span><span class="o">.</span><span class="n">password</span> <span class="o">=</span> <span class="s2">&quot;-=VP2001=-&quot;</span>   <span class="c1">#старый пароль был таки ненадежен</span>
</pre></div>
<p>Сессия внимательно следит за нами. Она, для примера, знает, что Вася был модифицирован:
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="n">session</span><span class="o">.</span><span class="n">dirty</span>
<span class="n">IdentitySet</span><span class="p">([</span><span class="o">&lt;</span><span class="n">User</span><span class="p">(</span><span class="s1">&#39;vasia&#39;</span><span class="p">,</span><span class="s1">&#39;Vasiliy Pypkin&#39;</span><span class="p">,</span> <span class="s1">&#39;-=VP2001=-&#39;</span><span class="p">)</span><span class="o">&gt;</span><span class="p">])</span>
</pre></div>
<p>И что еще пара User’ов ожидают сброса в базу:
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="n">session</span><span class="o">.</span><span class="n">new</span>
<span class="n">IdentitySet</span><span class="p">([</span><span class="o">&lt;</span><span class="n">User</span><span class="p">(</span><span class="s1">&#39;kolia&#39;</span><span class="p">,</span><span class="s1">&#39;Cool Kolian[S.A.]&#39;</span><span class="p">,</span> <span class="s1">&#39;kolia$$$&#39;</span><span class="p">)</span><span class="o">&gt;</span><span class="p">,</span> <span class="o">&lt;</span><span class="n">User</span><span class="p">(</span><span class="s1">&#39;zina&#39;</span><span class="p">,</span><span class="s1">&#39;Zina Korzina&#39;</span><span class="p">,</span> <span class="s1">&#39;zk18&#39;</span><span class="p">)</span><span class="o">&gt;</span><span class="p">])</span>
</pre></div>
<p>А теперь мы скажем нашей сессии, что мы хотим отправить все оставшиеся изменения в базу и применить все изменения, зафиксировав транзакцию, которая до того была в процессе. Это делается с помощью <i>commit()</i>:
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="n">session</span><span class="o">.</span><span class="n">commit</span><span class="p">()</span>
</pre></div>
</p>
<h5><span id=".D0.9E.D1.82.D0.BA.D0.B0.D1.82_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B9"></span><span class="mw-headline" id="Откат_изменений">Откат изменений.
  <p></p>
<p>Учитывая то, что сессия работает с транзакциями, мы можем откатить сделанные изменения. Давайте внесем два изменения, которые затем мы откатим; поменяем имя пользователя vasiaUser на Vaska:
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="n">vasiaUser</span><span class="o">.</span><span class="n">name</span> <span class="o">=</span> <span class="s1">&#39;Vaska&#39;</span>
</pre></div>
<p>и добавим ошибочного пользователя, fake_user:
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="n">fake_user</span> <span class="o">=</span> <span class="n">User</span><span class="p">(</span><span class="s1">&#39;fakeuser&#39;</span><span class="p">,</span> <span class="s1">&#39;Invalid&#39;</span><span class="p">,</span> <span class="s1">&#39;12345&#39;</span><span class="p">)</span>
<span class="n">session</span><span class="o">.</span><span class="n">add</span><span class="p">(</span><span class="n">fake_user</span><span class="p">)</span>
</pre></div>
<p>Откатывая, мы видим, что имя vasiaUser опять стало vasia, и fake_user был удален из транзакции:
</p>
<div class="mw-highlight mw-content-ltr" dir="ltr"><pre><span></span><span class="n">session</span><span class="o">.</span><span class="n">rollback</span><span class="p">()</span>

<span class="n">vasiaUser</span><span class="o">.</span><span class="n">name</span> 
<span class="c1"># u&#39;vasia&#39;</span>
<span class="n">fake_user</span> <span class="ow">in</span> <span class="n">session</span>
<span class="c1"># False</span>
</pre></div>
<p></p>
</div></body>
</html>
