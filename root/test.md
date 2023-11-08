---
layout: page
title: "https://baptmania.github.io"
permalink: /test/
---
[[Projet Alternance]] #Projet_Alternance #IHM

![[EncoInterface.py]] ![[Bibliothèque_Perso.py]]

Objectif
L'objectif de l'Interface Homme Machine est de faire le lien entre les actions de l'humain et celles de la machine. Elle permet donc à l'utilisateur de demander au programme de réaliser une action précise ou d'entrer certains paramètres manuellement, alors que le programme est déjà en cours d'utilisation. L'IHM permet également à l'utilisateur de voir le programme en action pour interagir avec lui de manière plus aisée.

Réflexion
Pour une IHM optimale, il est important de bien réfléchir à son organisation. En effet, il est impératif que l'IHM soit intuitive pour que les utilisateurs puissent l'utiliser à son plein potentiel sans difficulté.

Celle-ci est, pour le moment, composée d'une seule fenêtre, qui elle possède 3 onglets. Chaque onglet à son propre rôle pour que l'utilisateur ne soit pas perdu.

Le premier onglet permet d'encoder toutes les images présentes dans le programme.
Le second onglet permet de lancer le programme de reconnaissance faciale.
Le dernier onglet permet d'ajouter un nouvel usager au programme en prenant soin de remplir toutes les informations ainsi qu'en prenant une photographie dudit usager.
Programmation
Imports
Pour débuter, nous devrons faire appel à toutes les librairies que nous auront besoin pour le bon fonctionnement du programme.

import tkinter as tk  
from tkcalendar import DateEntry  
from tkinter import ttk  
from tkinter.messagebox import showerror  
from PIL import ImageTk  
from PIL import Image  
import time  
from functools import partial  
from encodeur_photo import *  
import ImageEncoding  
import FacialRecognition  
import Picture
La classe App
Le programme sera une application et celle-ci nécessite une classe.

Initialisation
Il faut donc tout d'abord initialiser la classe avec toutes les variables dont elle a besoin, ses variables de configuration et l'exécution des méthodes obligatoires.

class App(tk.Tk):  
    """Application d'encodage de photographies et de reconnaissance faciale"""  

    def __init__(self):  
        super().__init__()  
        #   Création des variables  
        self._tab1 = None  
        self._tab2 = None  
        self._tab3 = None  
        self._header_image_encoding = None  
        self._button_ImageEncoding = None  
        self._body_image_encoding = None  
        self.text_image_encoding = None  
        self._footer_image_encoding = None  
        self._exit_button = None  
        self._header_facial_recognition = None  
        self._button_facial_recognition = None  
        self._button_facial_recognition_terminate = None  
        self._body_facial_recognition = None  
        self._picture_facial_recognition = None  
        self.text_facial_recognition = None  
        self._footer_facial_recognition = None  
        self._header_picture = None  
        self._first_name_picture = None  
        self._first_name_picture_var = None  
        self._first_name_picture_entry = None  
        self._last_name_picture = None  
        self._last_name_picture_var = None  
        self._last_name_picture_entry = None  
        self._status_picture = None  
        self._status_picture_var = None  
        self._status_picture_entry = None  
        self._birthday_picture = None  
        self._birthday = None  
        self._button_picture = None  
        self._button_save_picture = None  
        self._body_picture = None  
        self._text_picture = None  
        self._picture_label = None  
        self._footer_picture = None  
        self._button_save = None  
        #   Configuration de la fenêtre principale  
        self.title("Outil de reconnaissance faciale")  
        self.geometry('730x625')  
        self.resizable(False, False)  
        self.tabcontrol = ttk.Notebook(self)  
        #   Configuration du style des différents Widgets  
        self.config(bg='#42495D')  
        self.s = ttk.Style()  
        self.s.configure('TFrame', background='#42495D')  
        self.s.configure('Header.TFrame', background='#42495D')  
        self.s.configure('Text.TFrame', background='#606C89')  
        self.s.configure('Body.TFrame', background='#42495D')  
        self.s.configure('Footer.TFrame', background='#42495D')  
        #   Lancement des procédures initiales  
        self.create_tab_1()  
        self.create_tab_2()  
        self.create_tab_3()
Les méthodes obligatoires
Les méthodes obligatoires sont ici la création des trois onglets de la fenêtre.

L'onglet 1 :
def create_tab_1(self):  
    self._tab1 = ttk.Frame(self.tabcontrol)  
    self.tabcontrol.add(self._tab1, text='Encodage')  
    self.tabcontrol.grid(row=0, column=0, sticky="nw")  
    self.create_header_frame_image_encoding()  
    self.create_body_frame_image_encoding()  
    self.create_footer_frame_image_encoding()
L'onglet 2 :
def create_tab_2(self):  
    self._tab2 = ttk.Frame(self.tabcontrol)  
    self.tabcontrol.add(self._tab2, text='Reconnaissance Faciale')  
    self.tabcontrol.grid(row=0, column=0, sticky="nw")  
    self.create_header_frame_facial_recognition()  
    self.create_body_frame_facial_recognition()  
    self.create_footer_frame_facial_recognition()
L'onglet 3 :
def create_tab_3(self):  
    self._tab3 = ttk.Frame(self.tabcontrol)  
    self.tabcontrol.add(self._tab3, text='Photographie')  
    self.tabcontrol.grid(row=0, column=0, sticky="nw")  
    self.create_header_picture()  
    self.create_body_picture()  
    self.create_footer_picture()
On remarquera que la création de chaque onglet implique la création d'un header, un body ainsi qu'un footer. Chaque onglet possède sa propre formation de page, ce qui implique à chaque fois d'écrire une nouvelle méthode pour créer un header, un body et un footer.

L'onglet 1
Pour commencer, on va d'abord ajouter un header à l'onglet.

def create_header_frame_image_encoding(self):  
    #   Premier onglet de l'application -- Encodage de l'image  
    self._header_image_encoding = ttk.Frame(self._tab1, style='Header.TFrame')  
    self._header_image_encoding.columnconfigure(0, weight=1)  

    self._button_ImageEncoding = tk.Button(self._header_image_encoding,  
                                           bg='#42495D',  
                                           fg='white',  
                                           relief='flat',  
                                           text="Encoder les photos")  
    self._button_ImageEncoding['command'] = self.handle_system_info  
    self._button_ImageEncoding.grid(column=0, row=0)  
    self._button_ImageEncoding.bind('<Enter>', set_color_on_mouse_over)  
    self._button_ImageEncoding.bind('<Leave>', set_color_on_mouse_leave)  

    self._header_image_encoding.grid(column=0, row=0, sticky=tk.NSEW, padx=10, pady=10)
Le header possède un bouton qui permet à l'utilisateur d'exécuter l'encodage des photographies des usagers. Pour cela, le bouton appelle une fonction qui permet de gérer l'action.

def handle_system_info(self):  
    self._button_ImageEncoding['state'] = tk.DISABLED  
    self.text_image_encoding.delete(1.0, "end")  

    _image_encoding_thread = ImageEncoding.ImageEncoding()  
    _image_encoding_thread.start()  
    self.image_encoding_monitor(_image_encoding_thread)
L'appel à cette méthode permet l'exécution du programme d'encodage des photographies. Le bouton pour exécuter le programme est bloquer pour éviter d'exécuter plusieurs fois le programme et de finir par bloquer l'ordinateur ou d'engendrer des erreurs lors de l'exécution. Ledit programme est exécuter sur un nouveau thread pour éviter de bloquer l'interface. Un thread créé depuis un programme doit être géré pour éviter qu'il tourne en fond sans pouvoir être arrêté. On créer donc une méthode qui va surveiller le thread.

def image_encoding_monitor(self, _thread):  
    if _thread.is_alive():  
        #   Vérifie le Thread tous les 100ms  
        self.text_image_encoding.delete(1.0, "end")  
        self.text_image_encoding.insert(1.0, _thread.text_image_encoding)  
        self.after(100, lambda: self.image_encoding_monitor(_thread))  
    else:  
        self.text_image_encoding.delete(1.0, "end")  
        self.text_image_encoding.insert(1.0, _thread.text_image_encoding)  
        self._button_ImageEncoding['state'] = tk.NORMAL
Cette méthode permet de vérifier si le thread est toujours en cours d'exécution. Si c'est le cas, la méthode va attendre 100ms puis va s'appeler elle-même. Sinon, la méthode permet de pouvoir de nouveau utiliser le bouton pour encoder les images. Le choix du temps d'attente est important. En effet, s'il est trop court, le programme consommera beaucoup de ressources inutilement. Cependant, s'il est trop long, le bouton sera bloqué longtemps inutilement aussi. La méthode permet également d'afficher du texte sur l'onglet pour pouvoir voir l'état d'avancement de l'exécution du programme.

On continuera ensuite avec l'ajout d'un body.

def create_body_frame_image_encoding(self):  
    self._body_image_encoding = ttk.Frame(self._tab1, style='Body.TFrame')  
    # text and scrollbar  
    self.text_image_encoding = tk.Text(self._body_image_encoding, height=20, bg='#606C89')  
    self.text_image_encoding.grid(column=0, row=1)  

    _scrollbar = ttk.Scrollbar(self._body_image_encoding,  
                              orient='vertical',  
                              command=self.text_image_encoding.yview)  
    _scrollbar.grid(column=1, row=1, sticky=tk.NS)  
    self.text_image_encoding['yscrollcommand'] = _scrollbar.set  

    # attach the body frame  
    self._body_image_encoding.grid(column=0, row=1, sticky=tk.NSEW, padx=10, pady=10)
Le body contient ici une zone de texte qui permet d'afficher à l'utilisateur l'état d'avancement de l'exécution de l'encodage des photographies. Une barre de scroll est présente pour le cas où le texte est long. Celle-ci est uniquement verticale. En effet, si le texte est trop long en largeur, il y aura un retour chariot.

On terminera alors avec un footer.

def create_footer_frame_image_encoding(self):  
    self._footer_image_encoding = ttk.Frame(self._tab1, style='Footer.TFrame')  
    # configure the grid  
    self._footer_image_encoding.columnconfigure(0, weight=1)  
    # exit button  
    self._exit_button = tk.Button(self._footer_image_encoding,  
                                  bg='#42495D',  
                                  fg='white',  
                                  relief='flat',  
                                  text='Quitter',  
                                  command=self.destroy)  
    self._exit_button.grid(column=0, row=0, sticky=tk.E)  
    self._exit_button.bind('<Enter>', set_color_on_mouse_over)  
    self._exit_button.bind('<Leave>', set_color_on_mouse_leave)  

    # attach the footer frame  
    self._footer_image_encoding.grid(column=0, row=2, sticky=tk.NSEW, padx=10, pady=10)
Le footer de cet onglet ne contient qu'un bouton pour permettre de quitter le programme.

L'onglet 2
Pour commencer, on va d'abord ajouter un header à l'onglet.

def create_header_frame_facial_recognition(self):  
    #   Deuxième onglet de l'application -- Reconnaissance Faciale  
    self._header_facial_recognition = ttk.Frame(self._tab2, style='Header.TFrame')  
    self._header_facial_recognition.columnconfigure(0, weight=1)  
    #   On demande si le programme doit être exécuté avec un CPU ou un GPU  
    _options = ["CPU", "GPU"]  
    _variable_menu = tk.StringVar(self._header_facial_recognition)  
    _variable_menu.set(_options[0])  
    _menu = tk.OptionMenu(self._header_facial_recognition, _variable_menu, *_options)  
    _menu.grid(column=1, row=0, sticky=tk.NSEW, padx=10, pady=10)  

    self._button_facial_recognition = tk.Button(self._header_facial_recognition,  
                                                bg='#42495D',  
                                                fg='white',  
                                                relief='flat',  
                                                text="Exécuter la reconnaissance faciale")  
    self._button_facial_recognition['command'] = self.handle_facial_recognition  
    self._button_facial_recognition.grid(column=0, row=0)  
    self._button_facial_recognition.bind('<Enter>', set_color_on_mouse_over)  
    self._button_facial_recognition.bind('<Leave>', set_color_on_mouse_leave)  

    self._header_facial_recognition.grid(column=0, row=0, sticky=tk.NSEW, padx=10, pady=10)
Le header permet ici de choisir le matériel d'exécution pour la reconnaissance faciale qui sont soit le CPU (par défaut) soit le GPU. Le CPU est choisi par défaut car toutes les machines ne possèdent pas de GPU. De plus, s'il y a eu une erreur lors de l'installation de CUDA, la reconnaissance faciale ne pourra pas être exécutée sur le GPU. Le header possède également un bouton qui permet à l'utilisateur d'exécuter la reconnaissance faciale. Pour cela, le bouton appelle une fonction qui permet de gérer l'action.

def handle_facial_recognition(self):  
    self._button_facial_recognition['state'] = tk.DISABLED  
    self.text_facial_recognition.delete(1.0, "end")  

    _facial_recognition_thread = FacialRecognition.FacialRecognition()  
    _facial_recognition_thread.start()  
    self.facial_recognition_monitor(_facial_recognition_thread)  

    self._button_facial_recognition_terminate = tk.Button(self._header_facial_recognition,  
                                                          bg='#42495D',  
                                                          fg='white',  
                                                          relief='flat',  
                                                          text="Arrêter la reconnaissance faciale")  
    self._button_facial_recognition_terminate['command'] = partial(self.handle_facial_recognition_terminate, _facial_recognition_thread)  
    self._button_facial_recognition_terminate.grid(column=1, row=0)  
    self._button_facial_recognition_terminate.bind('<Enter>', set_color_on_mouse_over)  
    self._button_facial_recognition_terminate.bind('<Leave>', set_color_on_mouse_leave)
L'appel à cette méthode permet l'exécution du programme de reconnaissance faciale. Le bouton pour exécuter le programme est bloquer pour éviter d'exécuter plusieurs fois le programme et de finir par bloquer l'ordinateur ou d'engendrer des erreurs lors de l'exécution. Ledit programme est exécuter sur un nouveau thread pour éviter de bloquer l'interface. Un thread créé depuis un programme doit être géré pour éviter qu'il tourne en fond sans pouvoir être arrêté. On créer donc une méthode qui va surveiller le thread.

def facial_recognition_monitor(self, _thread):  
    if _thread.is_alive():  
        # check the thread every 100ms.  
        self.text_facial_recognition.delete(1.0, "end")  
        _text = _thread.get_text()  
        self.text_facial_recognition.insert(1.0, _text)  
        if _thread.picture is not None:  
            self._text_picture.delete(1.0, "end")  
            _photo = ImageTk.PhotoImage(Image.fromarray(_thread.picture))  

            # Configurez votre label Tkinter pour afficher l'image  
            self._picture_facial_recognition.configure(image=_photo)  
            self._picture_facial_recognition.image = _photo  
        self.after(100, lambda: self.facial_recognition_monitor(_thread))  
    else:  
        self.text_facial_recognition.delete(1.0, "end")  
        _text = _thread.get_text()  
        self.text_facial_recognition.insert(1.0, _text)  
        self._button_facial_recognition['state'] = tk.NORMAL
Cette méthode permet de vérifier si le thread est toujours en cours d'exécution. Si c'est le cas, la méthode va attendre 100ms puis va s'appeler elle-même. Sinon, la méthode permet de pouvoir de nouveau utiliser le bouton pour reconnaître les visages. Le choix du temps d'attente est important. En effet, s'il est trop court, le programme consommera beaucoup de ressources inutilement. Cependant, s'il est trop long, le bouton sera bloqué longtemps inutilement aussi. La méthode permet également d'afficher du texte sur l'onglet pour pouvoir voir l'état d'avancement de l'exécution du programme.

Un second bouton a été créé sur le header pour pouvoir stopper la reconnaissance faciale. En effet, le programme de la reconnaissance faciale est un programme qui s'exécute sans s'arrêter. Celui-ci doit donc être arrêté manuellement.

def handle_facial_recognition_terminate(self, _thread):  
    _thread.set_terminate(True)  
    self._button_facial_recognition_terminate['state'] = tk.DISABLED
On continuera ensuite avec l'ajout d'un body.

def create_body_frame_facial_recognition(self):  
    self._body_facial_recognition = ttk.Frame(self._tab2, style='Body.TFrame')  

    self._picture_facial_recognition = tk.Label(self._body_facial_recognition)  
    self._picture_facial_recognition.grid(column=0, row=0)  
    _image = Image.open("black_font.png")  
    _img = ImageTk.PhotoImage(_image)  
    self._picture_facial_recognition['image'] = _img  

    # text and scrollbar  
    self.text_facial_recognition = tk.Text(self._body_facial_recognition, height=20, bg='#606C89')  
    self.text_facial_recognition.grid(column=0, row=1)  

    scrollbar = ttk.Scrollbar(self._body_facial_recognition,  
                              orient='vertical',  
                              command=self.text_facial_recognition.yview)  
    scrollbar.grid(column=1, row=1, sticky=tk.NS)  
    self.text_facial_recognition['yscrollcommand'] = scrollbar.set  

    # attach the body frame  
    self._body_facial_recognition.grid(column=0, row=1, sticky=tk.NSEW, padx=10, pady=10)
Le body contient ici une zone de texte qui permet d'afficher à l'utilisateur l'état d'avancement de l'exécution de la reconnaissance faciale. Une barre de scroll est présente pour le cas où le texte est long. Celle-ci est uniquement verticale. En effet, si le texte est trop long en largeur, il y aura un retour chariot.

On terminera alors avec un footer.

def create_footer_frame_facial_recognition(self):  
    self._footer_facial_recognition = ttk.Frame(self._tab2, style='Footer.TFrame')  
    # configure the grid  
    self._footer_facial_recognition.columnconfigure(0, weight=1)  
    # exit button  
    self._exit_button = tk.Button(self._footer_facial_recognition,  
                                  bg='#42495D',  
                                  fg='white',  
                                  relief='flat',  
                                  text='Quitter',  
                                  command=self.destroy)  
    self._exit_button.grid(column=0, row=0, sticky=tk.E)  
    self._exit_button.bind('<Enter>', set_color_on_mouse_over)  
    self._exit_button.bind('<Leave>', set_color_on_mouse_leave)  

    # attach the footer frame  
    self._footer_facial_recognition.grid(column=0, row=2, sticky=tk.NSEW, padx=10, pady=10)
Le footer de cet onglet ne contient qu'un bouton pour permettre de quitter le programme.

L'onglet 3
Pour commencer, on va d'abord ajouter un header à l'onglet.

def create_header_picture(self):  
    #   Troisième onglet de l'application -- Ajout d'une personne  
    self._header_picture = ttk.Frame(self._tab3, style='Header.TFrame')  
    self._header_picture.columnconfigure(0, weight=1)  

    # configure the grid  
    self._header_picture.columnconfigure(0, weight=1)  
    self._header_picture.columnconfigure(1, weight=10)  
    self._header_picture.columnconfigure(2, weight=1)  

    # label  
    self._first_name_picture = tk.Label(self._header_picture, text='Prénom ', bg='#42495D', fg='white')  
    self._first_name_picture.grid(column=0, row=0, sticky=tk.W)  

    # entry  
    self._first_name_picture_var = tk.StringVar()  
    self._first_name_picture_entry = tk.Entry(self._header_picture,  
                                              textvariable=self._first_name_picture_var,  
                                              bg='#606C89', fg='white', width=80)  

    self._first_name_picture_entry.grid(column=1, row=0, sticky=tk.EW)  

    self._last_name_picture = tk.Label(self._header_picture, text='Nom ', bg='#42495D', fg='white')  
    self._last_name_picture.grid(column=0, row=1, sticky=tk.W)  

    # entry  
    self._last_name_picture_var = tk.StringVar()  
    self._last_name_picture_entry = tk.Entry(self._header_picture,  
                                             textvariable=self._last_name_picture_var,  
                                             bg='#606C89', fg='white', width=80)  

    self._last_name_picture_entry.grid(column=1, row=1, sticky=tk.EW)  

    self._birthday_picture = tk.Label(self._header_picture, text='Date de naissance ', bg='#42495D', fg='white')  
    self._birthday_picture.grid(column=0, row=2, sticky=tk.W)  

    sel = tk.StringVar()  
    cal = DateEntry(self._header_picture, selectmode='day', locale='fr_FR.UTF-8', textvariable=sel,  
                    date_pattern='dd/mm/yyyy')  
    cal.grid(column=1, row=2, sticky=tk.W)  
    self._birthday = {"Year": 0, "Month": 0, "Day": 0, "Verification": False}  
    sel.trace('w', partial(set_birthday_picture, self._birthday, sel))  

    self._status_picture = tk.Label(self._header_picture, text='Statut au Centre ', bg='#42495D', fg='white')  
    self._status_picture.grid(column=0, row=3, sticky=tk.W)  

    # entry  
    self._status_picture_var = tk.StringVar()  
    self._status_picture_entry = tk.Entry(self._header_picture,  
                                          textvariable=self._status_picture_var,  
                                          bg='#606C89', fg='white', width=80)  

    self._status_picture_entry.grid(column=1, row=3, sticky=tk.EW)  

    self._button_picture = tk.Button(self._header_picture,  
                                     bg='#42495D',  
                                     fg='white',  
                                     relief='flat',  
                                     text="Prendre photographie")  
    self._button_picture['command'] = self.handle_picture  
    self._button_picture.grid(column=2, row=0)  
    self._button_picture.bind('<Enter>', set_color_on_mouse_over)  
    self._button_picture.bind('<Leave>', set_color_on_mouse_leave)  

    self._header_picture.grid(column=0, row=0, sticky=tk.NSEW, padx=10, pady=10)
def set_birthday_picture(birthday, selection, *args):  
    if birthday["Verification"]:  
        birthday["Verification"] = False  
        selected_text = selection.get()[6:10]  
        if selected_text.isdigit():  
            birthday["Year"] = int(selected_text)  
        selected_text = selection.get()[3:5]  
        if selected_text.isdigit():  
            birthday["Month"] = int(selected_text)  
        selected_text = selection.get()[:2]  
        if selected_text.isdigit():  
            birthday["Day"] = int(selected_text)  
    else:  
        birthday["Verification"] = True
On continuera ensuite avec l'ajout d'un body.

def create_body_picture(self):  
    self._body_picture = ttk.Frame(self._tab3, style='Body.TFrame')  
    self._picture_label = tk.Label(self._header_picture)  
    self._picture_label.grid(column=1, row=4)  
    _image = Image.open("black_font.png")  
    _img = ImageTk.PhotoImage(_image)  
    self._picture_label['image'] = _img  
    # text and scrollbar  
    self._text_picture = tk.Text(self._body_picture, height=20, bg='#606C89')  
    self._text_picture.grid(column=0, row=1)  

    scrollbar = ttk.Scrollbar(self._body_picture,  
                              orient='vertical',  
                              command=self._text_picture.yview)  
    scrollbar.grid(column=1, row=1, sticky=tk.NS)  
    self._text_picture['yscrollcommand'] = scrollbar.set  

    # attach the body frame  
    self._body_picture.grid(column=0, row=1, sticky=tk.NSEW, padx=10, pady=10)
Le body contient ici une zone de texte qui permet d'afficher à l'utilisateur l'état d'avancement de l'exécution de l'ajout d'un usager. Une barre de scroll est présente pour le cas où le texte est long. Celle-ci est uniquement verticale. En effet, si le texte est trop long en largeur, il y aura un retour chariot.

On terminera alors avec un footer.

def create_footer_picture(self):  
    self._footer_picture = ttk.Frame(self._tab3, style='Footer.TFrame')  
    # configure the grid  
    self._footer_picture.columnconfigure(0, weight=1)  

    self._button_save = tk.Button(self._footer_picture,  
                                  bg='#42495D',  
                                  fg='white',  
                                  relief='flat',  
                                  text="Enregistrer")  
    self._button_save['command'] = self.handle_save  
    self._button_save.grid(column=0, row=0)  
    self._button_save.bind('<Enter>', set_color_on_mouse_over)  
    self._button_save.bind('<Leave>', set_color_on_mouse_leave)  

    # exit button  
    self._exit_button = tk.Button(self._footer_picture,  
                                  bg='#42495D',  
                                  fg='white',  
                                  relief='flat',  
                                  text='Quitter',  
                                  command=self.destroy)  
    self._exit_button.grid(column=1, row=0, sticky=tk.E)  
    self._exit_button.bind('<Enter>', set_color_on_mouse_over)  
    self._exit_button.bind('<Leave>', set_color_on_mouse_leave)  

    # attach the footer frame  
    self._footer_picture.grid(column=0, row=2, sticky=tk.NSEW, padx=10, pady=10)
Le footer de cet onglet contient un bouton pour permettre de quitter le programme ainsi qu'un bouton pour enregistrer les informations entrées dans le header.

def handle_save(self):  
    _first_name = self._first_name_picture_var.get()  
    _last_name = self._last_name_picture_var.get()  
    _status = self._status_picture_var.get()  
    _birthday = self._birthday  
    if _first_name and _last_name and _birthday["Year"] and _status:  
        _year, _month, _day = _birthday["Year"], _birthday["Month"], _birthday["Day"]  
        _actual_year = int(datetime.datetime.now().strftime("%Y"))  
        _actual_month = int(datetime.datetime.now().strftime("%m"))  
        _actual_day = int(datetime.datetime.now().strftime("%d"))  
        if (_actual_month == _month and _actual_day < _day) or _actual_month <= _month: 
            _age = _actual_year - _year - 1  
        else:  
            _age = _actual_year - _year
        self._text_picture.delete(1.0, "end")  
        self._text_picture.insert(1.0,  
                                  f"Nom : {_last_name}\nPrénom : {_first_name}\nÂge : {_age}\nDate de naissance : {_day}/{_month}/{_year}\nLe statut de {_first_name} au Centre est {_status}")  
    else:  
        showerror(title='Erreur',  
                  message='Veuillez d\'abord indiquer toutes les informations avant d\'enregistrer les informations.')
Les informations sont vérifiées puis affichées dans le body.
