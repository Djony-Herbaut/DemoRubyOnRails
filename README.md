# **Projet de démonstation RubyOnRails**
---

### 🔧 **1. Créer un projet Rails**
```bash
sudo rails new DemoRubyOnRails
cd DemoRubyOnRails
```

---

### 📦 **2. Installer les dépendances**
```bash
sudo bundle install
```

---

### 🛠 **3. Générer un modèle, un contrôleur et une vue**
On va créer un modèle simple `Article` avec un titre et un contenu.

#### 3.1 Générer le modèle  
```bash
sudo rails generate model Article title:string content:text
```

#### 3.2 Appliquer la migration  
```bash
sudo rails db:migrate
```

#### 3.3 Générer un contrôleur pour gérer les articles  
```bash
sudo rails generate controller Articles
```

---

### ✍ **4. Configurer les routes**
Ouvre le fichier `config/routes.rb` et ajoute cette ligne à l'intérieur du `draw` :
```ruby
resources :articles
root "articles#index"
```
Cela crée les routes pour les articles et définit la page d'accueil sur `articles#index`.

---

### 🖥 **5. Implémenter les actions du contrôleur**
Puis on modifie notre `app/controllers/articles_controller.rb` pour y mettre du contenu minimal :
```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
    @article = Article.new
  end

  def create
    @article = Article.new(article_params)
    if @article.save
      redirect_to @article
    else
      render :new
    end
  end

  private

  def article_params
    params.require(:article).permit(:title, :content)
  end
end
```

---

### 🎨 **6. Créer les vues**
Dans `app/views/articles/`, crée ces fichiers :

#### **6.1 `index.html.erb`** (liste des articles)
```erb
<h1>Articles</h1>
<ul>
  <% @articles.each do |article| %>
    <li>
      <a href="<%= article_path(article) %>"><%= article.title %></a>
    </li>
  <% end %>
</ul>
<a href="<%= new_article_path %>">Créer un nouvel article</a>
```

#### **6.2 `show.html.erb`** (affichage d’un article)
```erb
<h1><%= @article.title %></h1>
<p><%= @article.content %></p>
<a href="<%= articles_path %>">Retour à la liste</a>
```

#### **6.3 `new.html.erb`** (formulaire de création)
```erb
<h1>Créer un nouvel article</h1>
<%= form_with model: @article, local: true do |form| %>
  <p>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
  </p>
  <p>
    <%= form.label :content %><br>
    <%= form.text_area :content %>
  </p>
  <p>
    <%= form.submit "Créer" %>
  </p>
<% end %>
<a href="<%= articles_path %>">Retour à la liste</a>
```

---

### 🚀 **7. Lancer le serveur**
```bash
sudo rails server
```
Puis, il faut ouvrir [http://localhost:3000](http://localhost:3000) dans ton navigateur. 🎉  

---

Maintenant, on a une **application ultra basique** qui illustre le fonctionnement de **MVC** avec RubyOnRails !
