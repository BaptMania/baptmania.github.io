---
layout: page
title: "https://baptmania.github.io"
permalink: /test/
---
<html>
    <head>
        <style>
            html{background-color: #10111A;}
            body{background-color: #1D2139;}
            h1{color: #37A9BE;}
            blockquote{color: #A954CA;}
            .lang-Python{background-color: #2B3051;}
            .hljs-keyword{color: #F3B549;}
        </style>
    </head>
<body>
    <h1 id="objectif">Objectif</h1>
    <blockquote>
        <p>L&#39;objectif de l&#39;Interface Homme Machine est de faire le lien entre les actions de l&#39;humain et celles de la machine. Elle permet donc à l&#39;utilisateur de demander au programme de réaliser une action précise ou d&#39;entrer certains paramètres manuellement, alors que le programme est déjà en cours d&#39;utilisation. L&#39;IHM permet également à l&#39;utilisateur de voir le programme en action pour interagir avec lui de manière plus aisée.</p>
    </blockquote>
    <h1 id="r-flexion">Réflexion</h1>
    <p>Pour une IHM optimale, il est important de bien réfléchir à son organisation. En effet, il est impératif que l&#39;IHM soit intuitive pour que les utilisateurs puissent l&#39;utiliser à son plein potentiel sans difficulté.</p>
    <p>Celle-ci est, pour le moment, composée d&#39;une seule fenêtre, qui elle possède 3 onglets. Chaque onglet à son propre rôle pour que l&#39;utilisateur ne soit pas perdu.</p>
    <ol>
        <li>Le premier onglet permet d&#39;encoder toutes les images présentes dans le programme. </li>
        <li>Le second onglet  permet de lancer le programme de reconnaissance faciale.</li>
        <li>Le dernier onglet permet d&#39;ajouter un nouvel usager au programme en prenant soin de remplir toutes les informations ainsi qu&#39;en prenant une photographie dudit usager.</li>
    </ol>
    <hr>
        <h1 id="programmation">Programmation</h1>
        <h3 id="imports">Imports</h3>
        <p>Pour débuter, nous devrons faire appel à toutes les librairies que nous auront besoin pour le bon fonctionnement du programme.</p>
        <pre>
            <code class="lang-Python">
                <span class="hljs-keyword">import</span> tkinter <span class="hljs-keyword">as</span> tk  
                <span class="hljs-keyword">from</span> tkcalendar <span class="hljs-keyword">import</span> DateEntry  
                <span class="hljs-keyword">from</span> tkinter <span class="hljs-keyword">import</span> ttk  
                <span class="hljs-keyword">from</span> tkinter.messagebox <span class="hljs-keyword">import</span> showerror  
                <span class="hljs-keyword">from</span> PIL <span class="hljs-keyword">import</span> ImageTk  
                <span class="hljs-keyword">from</span> PIL <span class="hljs-keyword">import</span> Image                      
                <span class="hljs-keyword">import</span> <span class="hljs-built_in">time</span> 
                <span class="hljs-keyword">from</span> functools <span class="hljs-keyword">import</span> partial 
                <span class="hljs-keyword">from</span> encodeur_photo <span class="hljs-keyword">import</span> *  
                <span class="hljs-keyword">import</span> ImageEncoding  
                <span class="hljs-keyword">import</span> FacialRecognition  
                <span class="hljs-keyword">import</span> Picture
            </code>
        </pre>
    <hr>
<h3 id="la-classe-app">La classe App</h3>
<p>Le programme sera une application et celle-ci nécessite une classe.</p>
<h4 id="initialisation">Initialisation</h4>
<p>Il faut donc tout d&#39;abord initialiser la classe avec toutes les variables dont elle a besoin, ses variables de configuration et l&#39;exécution des méthodes obligatoires.</p>
<pre><code class="lang-Python">class App(tk.Tk):  
    <span class="hljs-string">""</span><span class="hljs-string">"Application d'encodage de photographies et de reconnaissance faciale"</span><span class="hljs-string">""</span>  

    def __init__(<span class="hljs-keyword">self</span>):  
        <span class="hljs-keyword">super</span>().__init__()  
        #   Création des variables  
        <span class="hljs-keyword">self</span>._tab1 = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._tab2 = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._tab3 = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._header_image_encoding = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._button_ImageEncoding = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._body_image_encoding = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>.text_image_encoding = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._footer_image_encoding = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._exit_button = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._header_facial_recognition = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._button_facial_recognition = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._button_facial_recognition_terminate = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._body_facial_recognition = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._picture_facial_recognition = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>.text_facial_recognition = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._footer_facial_recognition = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._header_picture = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._first_name_picture = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._first_name_picture_var = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._first_name_picture_entry = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._last_name_picture = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._last_name_picture_var = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._last_name_picture_entry = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._status_picture = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._status_picture_var = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._status_picture_entry = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._birthday_picture = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._birthday = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._button_picture = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._button_save_picture = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._body_picture = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._text_picture = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._picture_label = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._footer_picture = <span class="hljs-literal">None</span>  
        <span class="hljs-keyword">self</span>._button_save = <span class="hljs-literal">None</span>  
        #   Configuration de la fenêtre principale  
        <span class="hljs-keyword">self</span>.title(<span class="hljs-string">"Outil de reconnaissance faciale"</span>)  
        <span class="hljs-keyword">self</span>.geometry('<span class="hljs-number">730</span>x625')  
        <span class="hljs-keyword">self</span>.resizable(False, False)  
        <span class="hljs-keyword">self</span>.tabcontrol = ttk.Notebook(<span class="hljs-keyword">self</span>)  
        #   Configuration du style des différents Widgets  
        <span class="hljs-keyword">self</span>.config(bg='#<span class="hljs-number">42495</span>D')  
        <span class="hljs-keyword">self</span>.s = ttk.Style()  
        <span class="hljs-keyword">self</span>.s.configure(<span class="hljs-symbol">'TFrame</span>', background='#<span class="hljs-number">42495</span>D')  
        <span class="hljs-keyword">self</span>.s.configure(<span class="hljs-symbol">'Header</span>.TFrame', background='#<span class="hljs-number">42495</span>D')  
        <span class="hljs-keyword">self</span>.s.configure(<span class="hljs-symbol">'Text</span>.TFrame', background='#<span class="hljs-number">606</span>C89')  
        <span class="hljs-keyword">self</span>.s.configure(<span class="hljs-symbol">'Body</span>.TFrame', background='#<span class="hljs-number">42495</span>D')  
        <span class="hljs-keyword">self</span>.s.configure(<span class="hljs-symbol">'Footer</span>.TFrame', background='#<span class="hljs-number">42495</span>D')  
        #   Lancement des <span class="hljs-keyword">proc</span>édures initiales  
        <span class="hljs-keyword">self</span>.create_tab_1()  
        <span class="hljs-keyword">self</span>.create_tab_2()  
        <span class="hljs-keyword">self</span>.create_tab_3()
</code></pre>
<hr>
<h4 id="les-m-thodes-obligatoires">Les méthodes obligatoires</h4>
<p>Les méthodes obligatoires sont ici la création des trois onglets de la fenêtre.</p>
<ol>
<li>L&#39;onglet 1 :</li>
</ol>
<pre><code class="lang-Python"><span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">create_tab_1</span><span class="hljs-params">(<span class="hljs-keyword">self</span>)</span></span>:  
    <span class="hljs-keyword">self</span>._tab1 = ttk.Frame(<span class="hljs-keyword">self</span>.tabcontrol)  
    <span class="hljs-keyword">self</span>.tabcontrol.add(<span class="hljs-keyword">self</span>._tab1, text=<span class="hljs-string">'Encodage'</span>)  
    <span class="hljs-keyword">self</span>.tabcontrol.grid(row=<span class="hljs-number">0</span>, column=<span class="hljs-number">0</span>, sticky=<span class="hljs-string">"nw"</span>)  
    <span class="hljs-keyword">self</span>.create_header_frame_image_encoding()  
    <span class="hljs-keyword">self</span>.create_body_frame_image_encoding()  
    <span class="hljs-keyword">self</span>.create_footer_frame_image_encoding()
</code></pre>
<ol>
<li>L&#39;onglet 2 :</li>
</ol>
<pre><code class="lang-Python"><span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">create_tab_2</span><span class="hljs-params">(<span class="hljs-keyword">self</span>)</span></span>:  
    <span class="hljs-keyword">self</span>._tab2 = ttk.Frame(<span class="hljs-keyword">self</span>.tabcontrol)  
    <span class="hljs-keyword">self</span>.tabcontrol.add(<span class="hljs-keyword">self</span>._tab2, text=<span class="hljs-string">'Reconnaissance Faciale'</span>)  
    <span class="hljs-keyword">self</span>.tabcontrol.grid(row=<span class="hljs-number">0</span>, column=<span class="hljs-number">0</span>, sticky=<span class="hljs-string">"nw"</span>)  
    <span class="hljs-keyword">self</span>.create_header_frame_facial_recognition()  
    <span class="hljs-keyword">self</span>.create_body_frame_facial_recognition()  
    <span class="hljs-keyword">self</span>.create_footer_frame_facial_recognition()
</code></pre>
<ol>
<li>L&#39;onglet 3 :</li>
</ol>
<pre><code class="lang-Python"><span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">create_tab_3</span><span class="hljs-params">(<span class="hljs-keyword">self</span>)</span></span>:  
    <span class="hljs-keyword">self</span>._tab3 = ttk.Frame(<span class="hljs-keyword">self</span>.tabcontrol)  
    <span class="hljs-keyword">self</span>.tabcontrol.add(<span class="hljs-keyword">self</span>._tab3, text=<span class="hljs-string">'Photographie'</span>)  
    <span class="hljs-keyword">self</span>.tabcontrol.grid(row=<span class="hljs-number">0</span>, column=<span class="hljs-number">0</span>, sticky=<span class="hljs-string">"nw"</span>)  
    <span class="hljs-keyword">self</span>.create_header_picture()  
    <span class="hljs-keyword">self</span>.create_body_picture()  
    <span class="hljs-keyword">self</span>.create_footer_picture()
</code></pre>
<blockquote>
<p>On remarquera que la création de chaque onglet implique la création d&#39;un header, un body ainsi qu&#39;un footer. Chaque onglet possède sa propre formation de page, ce qui implique à chaque fois d&#39;écrire une nouvelle méthode pour créer un header, un body et un footer.</p>
</blockquote>
<hr>
<h4 id="l-onglet-1">L&#39;onglet 1</h4>
<p>Pour commencer, on va d&#39;abord ajouter un header à l&#39;onglet.</p>
<pre><code class="lang-Python"><span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">create_header_frame_image_encoding</span><span class="hljs-params">(<span class="hljs-keyword">self</span>)</span></span>:  
    <span class="hljs-comment">#   Premier onglet de l'application -- Encodage de l'image  </span>
    <span class="hljs-keyword">self</span>._header_image_encoding = ttk.Frame(<span class="hljs-keyword">self</span>._tab1, style=<span class="hljs-string">'Header.TFrame'</span>)  
    <span class="hljs-keyword">self</span>._header_image_encoding.columnconfigure(<span class="hljs-number">0</span>, weight=<span class="hljs-number">1</span>)  

    <span class="hljs-keyword">self</span>._button_ImageEncoding = tk.Button(<span class="hljs-keyword">self</span>._header_image_encoding,  
                                           bg=<span class="hljs-string">'#42495D'</span>,  
                                           fg=<span class="hljs-string">'white'</span>,  
                                           relief=<span class="hljs-string">'flat'</span>,  
                                           text=<span class="hljs-string">"Encoder les photos"</span>)  
    <span class="hljs-keyword">self</span>._button_ImageEncoding[<span class="hljs-string">'command'</span>] = <span class="hljs-keyword">self</span>.handle_system_info  
    <span class="hljs-keyword">self</span>._button_ImageEncoding.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">0</span>)  
    <span class="hljs-keyword">self</span>._button_ImageEncoding.bind(<span class="hljs-string">'&lt;Enter&gt;'</span>, set_color_on_mouse_over)  
    <span class="hljs-keyword">self</span>._button_ImageEncoding.bind(<span class="hljs-string">'&lt;Leave&gt;'</span>, set_color_on_mouse_leave)  

    <span class="hljs-keyword">self</span>._header_image_encoding.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">0</span>, sticky=tk.NSEW, padx=<span class="hljs-number">10</span>, pady=<span class="hljs-number">10</span>)
</code></pre>
<p>Le header possède un bouton qui permet à l&#39;utilisateur d&#39;exécuter l&#39;encodage des photographies des usagers. Pour cela, le bouton appelle une fonction qui permet de gérer l&#39;action.</p>
<pre><code class="lang-Python">def handle_system_info(<span class="hljs-literal">self</span>):  
    <span class="hljs-literal">self</span>._button_ImageEncoding['<span class="hljs-keyword">state</span>'] = tk.DISABLED  
    <span class="hljs-literal">self</span>.text_image_encoding.delete(<span class="hljs-number">1.0</span>, <span class="hljs-string">"end"</span>)  

    _image_encoding_thread = ImageEncoding.ImageEncoding()  
    _image_encoding_thread.start()  
    <span class="hljs-literal">self</span>.image_encoding_monitor(_image_encoding_thread)
</code></pre>
<p>L&#39;appel à cette méthode permet l&#39;exécution du programme d&#39;encodage des photographies. Le bouton pour exécuter le programme est bloquer pour éviter d&#39;exécuter plusieurs fois le programme et de finir par bloquer l&#39;ordinateur ou d&#39;engendrer des erreurs lors de l&#39;exécution. Ledit programme est exécuter sur un nouveau <em>thread</em> pour éviter de bloquer l&#39;interface. Un <em>thread</em> créé depuis un programme doit être géré pour éviter qu&#39;il tourne en fond sans pouvoir être arrêté. On créer donc une méthode qui va surveiller le <em>thread</em>.</p>
<pre><code class="lang-Python"><span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">image_encoding_monitor</span><span class="hljs-params">(<span class="hljs-keyword">self</span>, _thread)</span></span>:  
    <span class="hljs-keyword">if</span> _thread.is_alive():  
        <span class="hljs-comment">#   Vérifie le Thread tous les 100ms  </span>
        <span class="hljs-keyword">self</span>.text_image_encoding.delete(<span class="hljs-number">1.0</span>, <span class="hljs-string">"end"</span>)  
        <span class="hljs-keyword">self</span>.text_image_encoding.insert(<span class="hljs-number">1.0</span>, _thread.text_image_encoding)  
        <span class="hljs-keyword">self</span>.after(<span class="hljs-number">100</span>, <span class="hljs-symbol">lambda:</span> <span class="hljs-keyword">self</span>.image_encoding_monitor(_thread))  
    <span class="hljs-symbol">else:</span>  
        <span class="hljs-keyword">self</span>.text_image_encoding.delete(<span class="hljs-number">1.0</span>, <span class="hljs-string">"end"</span>)  
        <span class="hljs-keyword">self</span>.text_image_encoding.insert(<span class="hljs-number">1.0</span>, _thread.text_image_encoding)  
        <span class="hljs-keyword">self</span>._button_ImageEncoding[<span class="hljs-string">'state'</span>] = tk.NORMAL
</code></pre>
<p>Cette méthode permet de vérifier si le <em>thread</em> est toujours en cours d&#39;exécution. Si c&#39;est le cas, la méthode va attendre 100ms puis va s&#39;appeler elle-même. Sinon, la méthode permet de pouvoir de nouveau utiliser le bouton pour encoder les images. Le choix du temps d&#39;attente est important. En effet, s&#39;il est trop court, le programme consommera beaucoup de ressources inutilement. Cependant, s&#39;il est trop long, le bouton sera bloqué longtemps inutilement aussi. La méthode permet également d&#39;afficher du texte sur l&#39;onglet pour pouvoir voir l&#39;état d&#39;avancement de l&#39;exécution du programme.</p>
<p>On continuera ensuite avec l&#39;ajout d&#39;un body.</p>
<pre><code class="lang-Python">def create_body_frame_image_encoding(self):  
    self.<span class="hljs-attr">_body_image_encoding</span> = ttk.Frame(self._tab1, <span class="hljs-attr">style='Body.TFrame')</span>  
    <span class="hljs-comment"># text and scrollbar  </span>
    self.<span class="hljs-attr">text_image_encoding</span> = tk.Text(self._body_image_encoding, <span class="hljs-attr">height=20,</span> <span class="hljs-attr">bg='#606C89')</span>  
    self.text_image_encoding.grid(<span class="hljs-attr">column=0,</span> <span class="hljs-attr">row=1)</span>  

    <span class="hljs-attr">_scrollbar</span> = ttk.Scrollbar(self._body_image_encoding,  
                              <span class="hljs-attr">orient='vertical',</span>  
                              <span class="hljs-attr">command=self.text_image_encoding.yview)</span>  
    _scrollbar.grid(<span class="hljs-attr">column=1,</span> <span class="hljs-attr">row=1,</span> <span class="hljs-attr">sticky=tk.NS)</span>  
    self.text_image_encoding['yscrollcommand'] = _scrollbar.set  

    <span class="hljs-comment"># attach the body frame  </span>
    self._body_image_encoding.grid(<span class="hljs-attr">column=0,</span> <span class="hljs-attr">row=1,</span> <span class="hljs-attr">sticky=tk.NSEW,</span> <span class="hljs-attr">padx=10,</span> <span class="hljs-attr">pady=10)</span>
</code></pre>
<p>Le body contient ici une zone de texte qui permet d&#39;afficher à l&#39;utilisateur l&#39;état d&#39;avancement de l&#39;exécution de l&#39;encodage des photographies. Une barre de scroll est présente pour le cas où le texte est long. Celle-ci est uniquement verticale. En effet, si le texte est trop long en largeur, il y aura un retour chariot.</p>
<p>On terminera alors avec un footer.</p>
<pre><code class="lang-Python"><span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">create_footer_frame_image_encoding</span><span class="hljs-params">(<span class="hljs-keyword">self</span>)</span></span>:  
    <span class="hljs-keyword">self</span>._footer_image_encoding = ttk.Frame(<span class="hljs-keyword">self</span>._tab1, style=<span class="hljs-string">'Footer.TFrame'</span>)  
    <span class="hljs-comment"># configure the grid  </span>
    <span class="hljs-keyword">self</span>._footer_image_encoding.columnconfigure(<span class="hljs-number">0</span>, weight=<span class="hljs-number">1</span>)  
    <span class="hljs-comment"># exit button  </span>
    <span class="hljs-keyword">self</span>._exit_button = tk.Button(<span class="hljs-keyword">self</span>._footer_image_encoding,  
                                  bg=<span class="hljs-string">'#42495D'</span>,  
                                  fg=<span class="hljs-string">'white'</span>,  
                                  relief=<span class="hljs-string">'flat'</span>,  
                                  text=<span class="hljs-string">'Quitter'</span>,  
                                  command=<span class="hljs-keyword">self</span>.destroy)  
    <span class="hljs-keyword">self</span>._exit_button.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">0</span>, sticky=tk.E)  
    <span class="hljs-keyword">self</span>._exit_button.bind(<span class="hljs-string">'&lt;Enter&gt;'</span>, set_color_on_mouse_over)  
    <span class="hljs-keyword">self</span>._exit_button.bind(<span class="hljs-string">'&lt;Leave&gt;'</span>, set_color_on_mouse_leave)  

    <span class="hljs-comment"># attach the footer frame  </span>
    <span class="hljs-keyword">self</span>._footer_image_encoding.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">2</span>, sticky=tk.NSEW, padx=<span class="hljs-number">10</span>, pady=<span class="hljs-number">10</span>)
</code></pre>
<p>Le footer de cet onglet ne contient qu&#39;un bouton pour permettre de quitter le programme. </p>
<hr>
<h4 id="l-onglet-2">L&#39;onglet 2</h4>
<p>Pour commencer, on va d&#39;abord ajouter un header à l&#39;onglet.</p>
<pre><code class="lang-Python"><span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">create_header_frame_facial_recognition</span><span class="hljs-params">(<span class="hljs-keyword">self</span>)</span></span>:  
    <span class="hljs-comment">#   Deuxième onglet de l'application -- Reconnaissance Faciale  </span>
    <span class="hljs-keyword">self</span>._header_facial_recognition = ttk.Frame(<span class="hljs-keyword">self</span>._tab2, style=<span class="hljs-string">'Header.TFrame'</span>)  
    <span class="hljs-keyword">self</span>._header_facial_recognition.columnconfigure(<span class="hljs-number">0</span>, weight=<span class="hljs-number">1</span>)  
    <span class="hljs-comment">#   On demande si le programme doit être exécuté avec un CPU ou un GPU  </span>
    _options = [<span class="hljs-string">"CPU"</span>, <span class="hljs-string">"GPU"</span>]  
    _variable_menu = tk.StringVar(<span class="hljs-keyword">self</span>._header_facial_recognition)  
    _variable_menu.set(_options[<span class="hljs-number">0</span>])  
    _menu = tk.OptionMenu(<span class="hljs-keyword">self</span>._header_facial_recognition, _variable_menu, *_options)  
    _menu.grid(column=<span class="hljs-number">1</span>, row=<span class="hljs-number">0</span>, sticky=tk.NSEW, padx=<span class="hljs-number">10</span>, pady=<span class="hljs-number">10</span>)  

    <span class="hljs-keyword">self</span>._button_facial_recognition = tk.Button(<span class="hljs-keyword">self</span>._header_facial_recognition,  
                                                bg=<span class="hljs-string">'#42495D'</span>,  
                                                fg=<span class="hljs-string">'white'</span>,  
                                                relief=<span class="hljs-string">'flat'</span>,  
                                                text=<span class="hljs-string">"Exécuter la reconnaissance faciale"</span>)  
    <span class="hljs-keyword">self</span>._button_facial_recognition[<span class="hljs-string">'command'</span>] = <span class="hljs-keyword">self</span>.handle_facial_recognition  
    <span class="hljs-keyword">self</span>._button_facial_recognition.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">0</span>)  
    <span class="hljs-keyword">self</span>._button_facial_recognition.bind(<span class="hljs-string">'&lt;Enter&gt;'</span>, set_color_on_mouse_over)  
    <span class="hljs-keyword">self</span>._button_facial_recognition.bind(<span class="hljs-string">'&lt;Leave&gt;'</span>, set_color_on_mouse_leave)  

    <span class="hljs-keyword">self</span>._header_facial_recognition.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">0</span>, sticky=tk.NSEW, padx=<span class="hljs-number">10</span>, pady=<span class="hljs-number">10</span>)
</code></pre>
<p>Le header permet ici de choisir le matériel d&#39;exécution pour la reconnaissance faciale qui sont soit le CPU <em>(par défaut)</em> soit le GPU. Le CPU est choisi par défaut car toutes les machines ne possèdent pas de GPU. De plus, s&#39;il y a eu une erreur lors de l&#39;installation de CUDA, la reconnaissance faciale ne pourra pas être exécutée sur le GPU.
Le header possède également un bouton qui permet à l&#39;utilisateur d&#39;exécuter la reconnaissance faciale. Pour cela, le bouton appelle une fonction qui permet de gérer l&#39;action.</p>
<pre><code class="lang-Python"><span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">handle_facial_recognition</span><span class="hljs-params">(<span class="hljs-keyword">self</span>)</span></span>:  
    <span class="hljs-keyword">self</span>._button_facial_recognition[<span class="hljs-string">'state'</span>] = tk.DISABLED  
    <span class="hljs-keyword">self</span>.text_facial_recognition.delete(<span class="hljs-number">1.0</span>, <span class="hljs-string">"end"</span>)  

    _facial_recognition_thread = FacialRecognition.FacialRecognition()  
    _facial_recognition_thread.start()  
    <span class="hljs-keyword">self</span>.facial_recognition_monitor(_facial_recognition_thread)  

    <span class="hljs-keyword">self</span>._button_facial_recognition_terminate = tk.Button(<span class="hljs-keyword">self</span>._header_facial_recognition,  
                                                          bg=<span class="hljs-string">'#42495D'</span>,  
                                                          fg=<span class="hljs-string">'white'</span>,  
                                                          relief=<span class="hljs-string">'flat'</span>,  
                                                          text=<span class="hljs-string">"Arrêter la reconnaissance faciale"</span>)  
    <span class="hljs-keyword">self</span>._button_facial_recognition_terminate[<span class="hljs-string">'command'</span>] = partial(<span class="hljs-keyword">self</span>.handle_facial_recognition_terminate, _facial_recognition_thread)  
    <span class="hljs-keyword">self</span>._button_facial_recognition_terminate.grid(column=<span class="hljs-number">1</span>, row=<span class="hljs-number">0</span>)  
    <span class="hljs-keyword">self</span>._button_facial_recognition_terminate.bind(<span class="hljs-string">'&lt;Enter&gt;'</span>, set_color_on_mouse_over)  
    <span class="hljs-keyword">self</span>._button_facial_recognition_terminate.bind(<span class="hljs-string">'&lt;Leave&gt;'</span>, set_color_on_mouse_leave)
</code></pre>
<p>L&#39;appel à cette méthode permet l&#39;exécution du programme de reconnaissance faciale. Le bouton pour exécuter le programme est bloquer pour éviter d&#39;exécuter plusieurs fois le programme et de finir par bloquer l&#39;ordinateur ou d&#39;engendrer des erreurs lors de l&#39;exécution. Ledit programme est exécuter sur un nouveau <em>thread</em> pour éviter de bloquer l&#39;interface. Un <em>thread</em> créé depuis un programme doit être géré pour éviter qu&#39;il tourne en fond sans pouvoir être arrêté. On créer donc une méthode qui va surveiller le <em>thread</em>.</p>
<pre><code class="lang-Python"><span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">facial_recognition_monitor</span><span class="hljs-params">(<span class="hljs-keyword">self</span>, _thread)</span></span>:  
    <span class="hljs-keyword">if</span> _thread.is_alive():  
        <span class="hljs-comment"># check the thread every 100ms.  </span>
        <span class="hljs-keyword">self</span>.text_facial_recognition.delete(<span class="hljs-number">1.0</span>, <span class="hljs-string">"end"</span>)  
        _text = _thread.get_text()  
        <span class="hljs-keyword">self</span>.text_facial_recognition.insert(<span class="hljs-number">1.0</span>, _text)  
        <span class="hljs-keyword">if</span> _thread.picture is <span class="hljs-keyword">not</span> <span class="hljs-symbol">None:</span>  
            <span class="hljs-keyword">self</span>._text_picture.delete(<span class="hljs-number">1.0</span>, <span class="hljs-string">"end"</span>)  
            _photo = ImageTk.PhotoImage(Image.fromarray(_thread.picture))  

            <span class="hljs-comment"># Configurez votre label Tkinter pour afficher l'image  </span>
            <span class="hljs-keyword">self</span>._picture_facial_recognition.configure(image=_photo)  
            <span class="hljs-keyword">self</span>._picture_facial_recognition.image = _photo  
        <span class="hljs-keyword">self</span>.after(<span class="hljs-number">100</span>, <span class="hljs-symbol">lambda:</span> <span class="hljs-keyword">self</span>.facial_recognition_monitor(_thread))  
    <span class="hljs-symbol">else:</span>  
        <span class="hljs-keyword">self</span>.text_facial_recognition.delete(<span class="hljs-number">1.0</span>, <span class="hljs-string">"end"</span>)  
        _text = _thread.get_text()  
        <span class="hljs-keyword">self</span>.text_facial_recognition.insert(<span class="hljs-number">1.0</span>, _text)  
        <span class="hljs-keyword">self</span>._button_facial_recognition[<span class="hljs-string">'state'</span>] = tk.NORMAL
</code></pre>
<p>Cette méthode permet de vérifier si le <em>thread</em> est toujours en cours d&#39;exécution. Si c&#39;est le cas, la méthode va attendre 100ms puis va s&#39;appeler elle-même. Sinon, la méthode permet de pouvoir de nouveau utiliser le bouton pour reconnaître les visages. Le choix du temps d&#39;attente est important. En effet, s&#39;il est trop court, le programme consommera beaucoup de ressources inutilement. Cependant, s&#39;il est trop long, le bouton sera bloqué longtemps inutilement aussi. La méthode permet également d&#39;afficher du texte sur l&#39;onglet pour pouvoir voir l&#39;état d&#39;avancement de l&#39;exécution du programme.</p>
<p>Un second bouton a été créé sur le header pour pouvoir stopper la reconnaissance faciale. En effet, le programme de la reconnaissance faciale est un programme qui s&#39;exécute sans s&#39;arrêter. Celui-ci doit donc être arrêté manuellement.</p>
<pre><code class="lang-Python">def handle_facial_recognition_terminate(<span class="hljs-literal">self</span>, _thread):  
    _thread.set_terminate(True)  
    <span class="hljs-literal">self</span>._button_facial_recognition_terminate['<span class="hljs-keyword">state</span>'] = tk.DISABLED
</code></pre>
<p>On continuera ensuite avec l&#39;ajout d&#39;un body.</p>
<pre><code class="lang-Python">def create_body_frame_facial_recognition(self):  
    self.<span class="hljs-attr">_body_facial_recognition</span> = ttk.Frame(self._tab2, <span class="hljs-attr">style='Body.TFrame')</span>  

    self.<span class="hljs-attr">_picture_facial_recognition</span> = tk.Label(self._body_facial_recognition)  
    self._picture_facial_recognition.grid(<span class="hljs-attr">column=0,</span> <span class="hljs-attr">row=0)</span>  
    <span class="hljs-attr">_image</span> = Image.open(<span class="hljs-string">"black_font.png"</span>)  
    <span class="hljs-attr">_img</span> = ImageTk.PhotoImage(_image)  
    self._picture_facial_recognition['image'] = _img  

    <span class="hljs-comment"># text and scrollbar  </span>
    self.<span class="hljs-attr">text_facial_recognition</span> = tk.Text(self._body_facial_recognition, <span class="hljs-attr">height=20,</span> <span class="hljs-attr">bg='#606C89')</span>  
    self.text_facial_recognition.grid(<span class="hljs-attr">column=0,</span> <span class="hljs-attr">row=1)</span>  

    <span class="hljs-attr">scrollbar</span> = ttk.Scrollbar(self._body_facial_recognition,  
                              <span class="hljs-attr">orient='vertical',</span>  
                              <span class="hljs-attr">command=self.text_facial_recognition.yview)</span>  
    scrollbar.grid(<span class="hljs-attr">column=1,</span> <span class="hljs-attr">row=1,</span> <span class="hljs-attr">sticky=tk.NS)</span>  
    self.text_facial_recognition['yscrollcommand'] = scrollbar.set  

    <span class="hljs-comment"># attach the body frame  </span>
    self._body_facial_recognition.grid(<span class="hljs-attr">column=0,</span> <span class="hljs-attr">row=1,</span> <span class="hljs-attr">sticky=tk.NSEW,</span> <span class="hljs-attr">padx=10,</span> <span class="hljs-attr">pady=10)</span>
</code></pre>
<p>Le body contient ici une zone de texte qui permet d&#39;afficher à l&#39;utilisateur l&#39;état d&#39;avancement de l&#39;exécution de la reconnaissance faciale. Une barre de scroll est présente pour le cas où le texte est long. Celle-ci est uniquement verticale. En effet, si le texte est trop long en largeur, il y aura un retour chariot.</p>
<p>On terminera alors avec un footer.</p>
<pre><code class="lang-Python"><span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">create_footer_frame_facial_recognition</span><span class="hljs-params">(<span class="hljs-keyword">self</span>)</span></span>:  
    <span class="hljs-keyword">self</span>._footer_facial_recognition = ttk.Frame(<span class="hljs-keyword">self</span>._tab2, style=<span class="hljs-string">'Footer.TFrame'</span>)  
    <span class="hljs-comment"># configure the grid  </span>
    <span class="hljs-keyword">self</span>._footer_facial_recognition.columnconfigure(<span class="hljs-number">0</span>, weight=<span class="hljs-number">1</span>)  
    <span class="hljs-comment"># exit button  </span>
    <span class="hljs-keyword">self</span>._exit_button = tk.Button(<span class="hljs-keyword">self</span>._footer_facial_recognition,  
                                  bg=<span class="hljs-string">'#42495D'</span>,  
                                  fg=<span class="hljs-string">'white'</span>,  
                                  relief=<span class="hljs-string">'flat'</span>,  
                                  text=<span class="hljs-string">'Quitter'</span>,  
                                  command=<span class="hljs-keyword">self</span>.destroy)  
    <span class="hljs-keyword">self</span>._exit_button.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">0</span>, sticky=tk.E)  
    <span class="hljs-keyword">self</span>._exit_button.bind(<span class="hljs-string">'&lt;Enter&gt;'</span>, set_color_on_mouse_over)  
    <span class="hljs-keyword">self</span>._exit_button.bind(<span class="hljs-string">'&lt;Leave&gt;'</span>, set_color_on_mouse_leave)  

    <span class="hljs-comment"># attach the footer frame  </span>
    <span class="hljs-keyword">self</span>._footer_facial_recognition.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">2</span>, sticky=tk.NSEW, padx=<span class="hljs-number">10</span>, pady=<span class="hljs-number">10</span>)
</code></pre>
<p>Le footer de cet onglet ne contient qu&#39;un bouton pour permettre de quitter le programme. </p>
<hr>
<h4 id="l-onglet-3">L&#39;onglet 3</h4>
<p>Pour commencer, on va d&#39;abord ajouter un header à l&#39;onglet.</p>
<pre><code class="lang-Python"><span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">create_header_picture</span><span class="hljs-params">(<span class="hljs-keyword">self</span>)</span></span>:  
    <span class="hljs-comment">#   Troisième onglet de l'application -- Ajout d'une personne  </span>
    <span class="hljs-keyword">self</span>._header_picture = ttk.Frame(<span class="hljs-keyword">self</span>._tab3, style=<span class="hljs-string">'Header.TFrame'</span>)  
    <span class="hljs-keyword">self</span>._header_picture.columnconfigure(<span class="hljs-number">0</span>, weight=<span class="hljs-number">1</span>)  

    <span class="hljs-comment"># configure the grid  </span>
    <span class="hljs-keyword">self</span>._header_picture.columnconfigure(<span class="hljs-number">0</span>, weight=<span class="hljs-number">1</span>)  
    <span class="hljs-keyword">self</span>._header_picture.columnconfigure(<span class="hljs-number">1</span>, weight=<span class="hljs-number">10</span>)  
    <span class="hljs-keyword">self</span>._header_picture.columnconfigure(<span class="hljs-number">2</span>, weight=<span class="hljs-number">1</span>)  

    <span class="hljs-comment"># label  </span>
    <span class="hljs-keyword">self</span>._first_name_picture = tk.Label(<span class="hljs-keyword">self</span>._header_picture, text=<span class="hljs-string">'Prénom '</span>, bg=<span class="hljs-string">'#42495D'</span>, fg=<span class="hljs-string">'white'</span>)  
    <span class="hljs-keyword">self</span>._first_name_picture.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">0</span>, sticky=tk.W)  

    <span class="hljs-comment"># entry  </span>
    <span class="hljs-keyword">self</span>._first_name_picture_var = tk.StringVar()  
    <span class="hljs-keyword">self</span>._first_name_picture_entry = tk.Entry(<span class="hljs-keyword">self</span>._header_picture,  
                                              textvariable=<span class="hljs-keyword">self</span>._first_name_picture_var,  
                                              bg=<span class="hljs-string">'#606C89'</span>, fg=<span class="hljs-string">'white'</span>, width=<span class="hljs-number">80</span>)  

    <span class="hljs-keyword">self</span>._first_name_picture_entry.grid(column=<span class="hljs-number">1</span>, row=<span class="hljs-number">0</span>, sticky=tk.EW)  

    <span class="hljs-keyword">self</span>._last_name_picture = tk.Label(<span class="hljs-keyword">self</span>._header_picture, text=<span class="hljs-string">'Nom '</span>, bg=<span class="hljs-string">'#42495D'</span>, fg=<span class="hljs-string">'white'</span>)  
    <span class="hljs-keyword">self</span>._last_name_picture.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">1</span>, sticky=tk.W)  

    <span class="hljs-comment"># entry  </span>
    <span class="hljs-keyword">self</span>._last_name_picture_var = tk.StringVar()  
    <span class="hljs-keyword">self</span>._last_name_picture_entry = tk.Entry(<span class="hljs-keyword">self</span>._header_picture,  
                                             textvariable=<span class="hljs-keyword">self</span>._last_name_picture_var,  
                                             bg=<span class="hljs-string">'#606C89'</span>, fg=<span class="hljs-string">'white'</span>, width=<span class="hljs-number">80</span>)  

    <span class="hljs-keyword">self</span>._last_name_picture_entry.grid(column=<span class="hljs-number">1</span>, row=<span class="hljs-number">1</span>, sticky=tk.EW)  

    <span class="hljs-keyword">self</span>._birthday_picture = tk.Label(<span class="hljs-keyword">self</span>._header_picture, text=<span class="hljs-string">'Date de naissance '</span>, bg=<span class="hljs-string">'#42495D'</span>, fg=<span class="hljs-string">'white'</span>)  
    <span class="hljs-keyword">self</span>._birthday_picture.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">2</span>, sticky=tk.W)  

    sel = tk.StringVar()  
    cal = DateEntry(<span class="hljs-keyword">self</span>._header_picture, selectmode=<span class="hljs-string">'day'</span>, locale=<span class="hljs-string">'fr_FR.UTF-8'</span>, textvariable=sel,  
                    date_pattern=<span class="hljs-string">'dd/mm/yyyy'</span>)  
    cal.grid(column=<span class="hljs-number">1</span>, row=<span class="hljs-number">2</span>, sticky=tk.W)  
    <span class="hljs-keyword">self</span>._birthday = {<span class="hljs-string">"Year"</span>: <span class="hljs-number">0</span>, <span class="hljs-string">"Month"</span>: <span class="hljs-number">0</span>, <span class="hljs-string">"Day"</span>: <span class="hljs-number">0</span>, <span class="hljs-string">"Verification"</span>: False}  
    sel.trace(<span class="hljs-string">'w'</span>, partial(set_birthday_picture, <span class="hljs-keyword">self</span>._birthday, sel))  

    <span class="hljs-keyword">self</span>._status_picture = tk.Label(<span class="hljs-keyword">self</span>._header_picture, text=<span class="hljs-string">'Statut au Centre '</span>, bg=<span class="hljs-string">'#42495D'</span>, fg=<span class="hljs-string">'white'</span>)  
    <span class="hljs-keyword">self</span>._status_picture.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">3</span>, sticky=tk.W)  

    <span class="hljs-comment"># entry  </span>
    <span class="hljs-keyword">self</span>._status_picture_var = tk.StringVar()  
    <span class="hljs-keyword">self</span>._status_picture_entry = tk.Entry(<span class="hljs-keyword">self</span>._header_picture,  
                                          textvariable=<span class="hljs-keyword">self</span>._status_picture_var,  
                                          bg=<span class="hljs-string">'#606C89'</span>, fg=<span class="hljs-string">'white'</span>, width=<span class="hljs-number">80</span>)  

    <span class="hljs-keyword">self</span>._status_picture_entry.grid(column=<span class="hljs-number">1</span>, row=<span class="hljs-number">3</span>, sticky=tk.EW)  

    <span class="hljs-keyword">self</span>._button_picture = tk.Button(<span class="hljs-keyword">self</span>._header_picture,  
                                     bg=<span class="hljs-string">'#42495D'</span>,  
                                     fg=<span class="hljs-string">'white'</span>,  
                                     relief=<span class="hljs-string">'flat'</span>,  
                                     text=<span class="hljs-string">"Prendre photographie"</span>)  
    <span class="hljs-keyword">self</span>._button_picture[<span class="hljs-string">'command'</span>] = <span class="hljs-keyword">self</span>.handle_picture  
    <span class="hljs-keyword">self</span>._button_picture.grid(column=<span class="hljs-number">2</span>, row=<span class="hljs-number">0</span>)  
    <span class="hljs-keyword">self</span>._button_picture.bind(<span class="hljs-string">'&lt;Enter&gt;'</span>, set_color_on_mouse_over)  
    <span class="hljs-keyword">self</span>._button_picture.bind(<span class="hljs-string">'&lt;Leave&gt;'</span>, set_color_on_mouse_leave)  

    <span class="hljs-keyword">self</span>._header_picture.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">0</span>, sticky=tk.NSEW, padx=<span class="hljs-number">10</span>, pady=<span class="hljs-number">10</span>)
</code></pre>
<pre><code class="lang-Python"><span class="hljs-symbol">def</span> set_birthday_picture(<span class="hljs-keyword">birthday, </span><span class="hljs-keyword">selection, </span>*args):  
    <span class="hljs-meta">if</span> <span class="hljs-keyword">birthday["Verification"]: </span> 
        <span class="hljs-keyword">birthday["Verification"] </span>= False  
        <span class="hljs-keyword">selected_text </span>= <span class="hljs-keyword">selection.get()[6:10] </span> 
        <span class="hljs-meta">if</span> <span class="hljs-keyword">selected_text.isdigit(): </span> 
            <span class="hljs-keyword">birthday["Year"] </span>= int(<span class="hljs-keyword">selected_text) </span> 
        <span class="hljs-keyword">selected_text </span>= <span class="hljs-keyword">selection.get()[3:5] </span> 
        <span class="hljs-meta">if</span> <span class="hljs-keyword">selected_text.isdigit(): </span> 
            <span class="hljs-keyword">birthday["Month"] </span>= int(<span class="hljs-keyword">selected_text) </span> 
        <span class="hljs-keyword">selected_text </span>= <span class="hljs-keyword">selection.get()[:2] </span> 
        <span class="hljs-meta">if</span> <span class="hljs-keyword">selected_text.isdigit(): </span> 
            <span class="hljs-keyword">birthday["Day"] </span>= int(<span class="hljs-keyword">selected_text) </span> 
<span class="hljs-symbol">    else:</span>  
        <span class="hljs-keyword">birthday["Verification"] </span>= True
</code></pre>
<p>On continuera ensuite avec l&#39;ajout d&#39;un body.</p>
<pre><code class="lang-Python">def create_body_picture(self):  
    self.<span class="hljs-attr">_body_picture</span> = ttk.Frame(self._tab3, <span class="hljs-attr">style='Body.TFrame')</span>  
    self.<span class="hljs-attr">_picture_label</span> = tk.Label(self._header_picture)  
    self._picture_label.grid(<span class="hljs-attr">column=1,</span> <span class="hljs-attr">row=4)</span>  
    <span class="hljs-attr">_image</span> = Image.open(<span class="hljs-string">"black_font.png"</span>)  
    <span class="hljs-attr">_img</span> = ImageTk.PhotoImage(_image)  
    self._picture_label['image'] = _img  
    <span class="hljs-comment"># text and scrollbar  </span>
    self.<span class="hljs-attr">_text_picture</span> = tk.Text(self._body_picture, <span class="hljs-attr">height=20,</span> <span class="hljs-attr">bg='#606C89')</span>  
    self._text_picture.grid(<span class="hljs-attr">column=0,</span> <span class="hljs-attr">row=1)</span>  

    <span class="hljs-attr">scrollbar</span> = ttk.Scrollbar(self._body_picture,  
                              <span class="hljs-attr">orient='vertical',</span>  
                              <span class="hljs-attr">command=self._text_picture.yview)</span>  
    scrollbar.grid(<span class="hljs-attr">column=1,</span> <span class="hljs-attr">row=1,</span> <span class="hljs-attr">sticky=tk.NS)</span>  
    self._text_picture['yscrollcommand'] = scrollbar.set  

    <span class="hljs-comment"># attach the body frame  </span>
    self._body_picture.grid(<span class="hljs-attr">column=0,</span> <span class="hljs-attr">row=1,</span> <span class="hljs-attr">sticky=tk.NSEW,</span> <span class="hljs-attr">padx=10,</span> <span class="hljs-attr">pady=10)</span>
</code></pre>
<p>Le body contient ici une zone de texte qui permet d&#39;afficher à l&#39;utilisateur l&#39;état d&#39;avancement de l&#39;exécution de l&#39;ajout d&#39;un usager. Une barre de scroll est présente pour le cas où le texte est long. Celle-ci est uniquement verticale. En effet, si le texte est trop long en largeur, il y aura un retour chariot.</p>
<p>On terminera alors avec un footer.</p>
<pre><code class="lang-Python"><span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">create_footer_picture</span><span class="hljs-params">(<span class="hljs-keyword">self</span>)</span></span>:  
    <span class="hljs-keyword">self</span>._footer_picture = ttk.Frame(<span class="hljs-keyword">self</span>._tab3, style=<span class="hljs-string">'Footer.TFrame'</span>)  
    <span class="hljs-comment"># configure the grid  </span>
    <span class="hljs-keyword">self</span>._footer_picture.columnconfigure(<span class="hljs-number">0</span>, weight=<span class="hljs-number">1</span>)  

    <span class="hljs-keyword">self</span>._button_save = tk.Button(<span class="hljs-keyword">self</span>._footer_picture,  
                                  bg=<span class="hljs-string">'#42495D'</span>,  
                                  fg=<span class="hljs-string">'white'</span>,  
                                  relief=<span class="hljs-string">'flat'</span>,  
                                  text=<span class="hljs-string">"Enregistrer"</span>)  
    <span class="hljs-keyword">self</span>._button_save[<span class="hljs-string">'command'</span>] = <span class="hljs-keyword">self</span>.handle_save  
    <span class="hljs-keyword">self</span>._button_save.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">0</span>)  
    <span class="hljs-keyword">self</span>._button_save.bind(<span class="hljs-string">'&lt;Enter&gt;'</span>, set_color_on_mouse_over)  
    <span class="hljs-keyword">self</span>._button_save.bind(<span class="hljs-string">'&lt;Leave&gt;'</span>, set_color_on_mouse_leave)  

    <span class="hljs-comment"># exit button  </span>
    <span class="hljs-keyword">self</span>._exit_button = tk.Button(<span class="hljs-keyword">self</span>._footer_picture,  
                                  bg=<span class="hljs-string">'#42495D'</span>,  
                                  fg=<span class="hljs-string">'white'</span>,  
                                  relief=<span class="hljs-string">'flat'</span>,  
                                  text=<span class="hljs-string">'Quitter'</span>,  
                                  command=<span class="hljs-keyword">self</span>.destroy)  
    <span class="hljs-keyword">self</span>._exit_button.grid(column=<span class="hljs-number">1</span>, row=<span class="hljs-number">0</span>, sticky=tk.E)  
    <span class="hljs-keyword">self</span>._exit_button.bind(<span class="hljs-string">'&lt;Enter&gt;'</span>, set_color_on_mouse_over)  
    <span class="hljs-keyword">self</span>._exit_button.bind(<span class="hljs-string">'&lt;Leave&gt;'</span>, set_color_on_mouse_leave)  

    <span class="hljs-comment"># attach the footer frame  </span>
    <span class="hljs-keyword">self</span>._footer_picture.grid(column=<span class="hljs-number">0</span>, row=<span class="hljs-number">2</span>, sticky=tk.NSEW, padx=<span class="hljs-number">10</span>, pady=<span class="hljs-number">10</span>)
</code></pre>
<p>Le footer de cet onglet contient un bouton pour permettre de quitter le programme ainsi qu&#39;un bouton pour enregistrer les informations entrées dans le header.</p>
<pre><code class="lang-Python">def handle_save(self):  
    _first_name = self._first_name_picture_var.<span class="hljs-built_in">get</span>()  
    _last_name = self._last_name_picture_var.<span class="hljs-built_in">get</span>()  
    _status = self._status_picture_var.<span class="hljs-built_in">get</span>()  
    _birthday = self._birthday  
    <span class="hljs-keyword">if</span> _first_name <span class="hljs-built_in">and</span> _last_name <span class="hljs-built_in">and</span> _birthday[<span class="hljs-string">"Year"</span>] <span class="hljs-built_in">and</span> _statu<span class="hljs-variable">s:</span>  
        _year, _month, _day = _birthday[<span class="hljs-string">"Year"</span>], _birthday[<span class="hljs-string">"Month"</span>], _birthday[<span class="hljs-string">"Day"</span>]  
        _actual_year = <span class="hljs-keyword">int</span>(datetime.datetime.now().<span class="hljs-built_in">strftime</span>(<span class="hljs-string">"%Y"</span>))  
        _actual_month = <span class="hljs-keyword">int</span>(datetime.datetime.now().<span class="hljs-built_in">strftime</span>(<span class="hljs-string">"%m"</span>))  
        _actual_day = <span class="hljs-keyword">int</span>(datetime.datetime.now().<span class="hljs-built_in">strftime</span>(<span class="hljs-string">"%d"</span>))  
        <span class="hljs-keyword">if</span> (_actual_month == _month <span class="hljs-built_in">and</span> _actual_day &lt; _day) <span class="hljs-built_in">or</span> _actual_month &lt;= _month: 
            _age = _actual_year - _year - <span class="hljs-number">1</span>  
        <span class="hljs-keyword">else</span>:  
            _age = _actual_year - _year
        self._text_picture.<span class="hljs-keyword">delete</span>(<span class="hljs-number">1.0</span>, <span class="hljs-string">"end"</span>)  
        self._text_picture.<span class="hljs-keyword">insert</span>(<span class="hljs-number">1.0</span>,  
                                  <span class="hljs-keyword">f</span><span class="hljs-string">"Nom : {_last_name}\nPrénom : {_first_name}\nÂge : {_age}\nDate de naissance : {_day}/{_month}/{_year}\nLe statut de {_first_name} au Centre est {_status}"</span>)  
    <span class="hljs-keyword">else</span>:  
        showerror(title=<span class="hljs-string">'Erreur'</span>,  
                  message=<span class="hljs-string">'Veuillez d\'abord indiquer toutes les informations avant d\'enregistrer les informations.'</span>)
</code></pre>
<p>Les informations sont vérifiées puis affichées dans le body.</p>
</body>
</html>
