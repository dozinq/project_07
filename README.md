# ๐ My Seventh Project ๐

---

##### - Outline : 2022๋ 4์ 15์ผ, ์ผ๊ณฑ๋ฒ์งธ ๊ดํต ํ๋ก์ ํธ๋ฅผ ์ํํ์๋ค. ํ ์ฃผ ์ ๊น์ง๋ง ํด๋ ์ค๋๋ง์ ์ํํ๋ ํ๋ก์ ํธ๋ผ์ ์ํฌ๋ฅด๊ฒ ์ํํ๋๋ฐ, ์ค๋์ ๊ทธ๋๋ ์์ํ๊ฒ ์ํํ  ์ ์์๋ค. ์ฌ์ค, ๊ทธ ๋ฐฐ๊ฒฝ์๋ ๋ค๋ฅธ ์ด์ ๊ฐ ์กด์ฌํ๋ค. ์ค๋๋ถํฐ ํ๋ก์ ํธ๋ ํ์ดํ๋ก์ ํธ๋ก ์ด๋ฃจ์ด์ก๊ณ , ์ค๋ก์ง ํ๋์ฌ๋ง์ด ํ๋ก์ ํธ๋ฅผ ์๋ฒฝํ๊ฒ ์ํํ  ์ ์๊ฒ ํด์ค๋ค๋ ๊ฒ์ ๋๋ ์ ์์๊ธฐ ๋๋ฌธ์ด๋ค. ๋์ ํ์ด๋ ๊ฐ์ ๋ฐ์ '์ ์ํ' ํ์ฐ์๋ค. ํ์์๋ ์นจ์ฐฉํ๊ฒ ๋ฌธ์  ํด๊ฒฐ์ ํ๋ ๊ฒ์ ์ ์๊ณ  ์์์ผ๋ฉฐ, ๋ช ๋ฒ ๋์๊ฒ ๋์์ ์ฃผ์๋ ํ์ฐ์ฌ์ ๊ณ ๋ง์ด ๋ง์์ ๊ฐ์ง๊ณ  ๋ณธ ํ๋ก์ ํธ์ ์ง์คํ๋ ค๊ณ  ํ์๋ค. ์ค๊ฐ ์ค๊ฐ ์ฌ๋ ์๊ฐ์ ์กฐ์จํ  ์๋ ์์ด์ ์ข์๋ ๊ฒ ๊ฐ๊ณ , ํฐ ์ค๋ฅ์์ด ํ๋ก์ ํธ๋ฅผ ๋ง์น  ์ ์์๋ค. ๋ง์น๊ณ  ๋์๋ ๋ด๊ฐ ๋ถ์กฑํ๋ฉด ํ์์ด ๊ฐ์ด ๊ณ ์ํ๋ค๋ ๊ฒ์ ๋ ํ ๋ฒ ๋๋ ์ ์์๋ ๊ฒ ๊ฐ์ผ๋ฉฐ, ๊ทธ๋ฌ๊ธฐ์ ๋ค์ ํ์ด๋ฅผ ์ํด์๋ ๋ด๊ฐ ๋ค์ ์ฃผ๋ ์ด์ฌํ ๊ณต๋ถํด์ผ ํ๋ค๊ณ  ์๊ฐ์ด ๋ค์๋ค. ์, ์ด์  ์ค๋์ ํ๋ก์ ํธ๋ฅผ ์ํํ๋ฉด์ ๋๊ผ๋ ์ ๊ณผ ๊ฐ์ ํด์ผ ํ  ์ ์ ์ค์ฌ์ผ๋ก README ํ์ผ์ ์์ฑํด๋ณด๋ ค ํ๋ค.

---

<br>


# **< Title : "์ฌ์ฉ์ ์ธ์ฆ๊ธฐ๋ฐ ๊ด๊ณํ DB ์ค๊ณ" >**

*(This project was carried out in **Python 3.9.9 and Django 3.2.12 environment .**)*

- *์๊ตฌ์ฌํญ : ์ด๋ ์ปค๋ฎค๋ํฐ ์๋น์ค์ ๊ฒ์ํ ๊ธฐ๋ฅ ๊ฐ๋ฐ์ ์ํ ๋จ๊ณ๋ก, ํด๋น ๊ธฐ๋ฅ๋ค์ ํฅํ ์ปค๋ฎค๋ํฐ ์๋น์ค์ ํ์ ๊ธฐ๋ฅ์ผ๋ก ์ฌ์ฉ๋  ๊ฒ์ด๋ผ๊ณ  ํ๋ค. ๋ช์ธ์์ ๊ธฐ์ ๋์ด ์๋ ์ฌํญ๋ค์ ํ์์ ์ผ๋ก ๊ตฌํํด์ผ ํ๋ค.*

---

*(ํ๋ก์ ํธ ํ์ผ์ settings.py, urls.py์ base.html ๋ฑ์ ๊ธฐ๋ณธ ์ค์ ์ ์ ์ธํ๊ณ  , ์ฑ ํ์ผ์ ๊ดํด์๋ง ์์ฑํฉ๋๋ค.)*

<br>

- **movies/urls.py**

  ```python
  from django.urls import path
  from . import views
  
  app_name = 'movies'
  urlpatterns = [
      path('', views.index, name='index'),
      path('create/', views.create, name='create'),
      path('<int:pk>/', views.detail, name='detail'),
      path('<int:pk>/delete/', views.delete, name='delete'),
      path('<int:pk>/update/', views.update, name='update'),
      path('<int:pk>/comments/', views.comment_create, name='comment_create'),
      path('<int:movie_pk>/comments/<int:comment_pk>/delete/', views.comment_delete, name='comment_delete'),
  ]
  ```
  
  : url์ ์๋ ฅํ์์ ๋, ํน์ ํด๋นurl๋ก์ ์ด๋์ ์ง์ ํด ์ค ๋์ ์ฌ๋ฐ๋ฅธ view ํจ์๊ฐ ์คํ๋  ์ ์๋๋ก ์ค์ ํด ์ฃผ์๋ค. ์ด๋ฅผ ์์ฑํ๋ฉด์ ์ค๋ฅ ์ฌํญ์ ์์๋ค. ๋ค๋ง, ๋ง์ง๋ง ์ค์ธ movie_pk์ comment_pk๋ฅผ ์์ฉํด์ผ ํ  ๋์๋ ํ์ด์ ํจ๊ป ๋ง์ ๊ณ ๋ฏผ์ ํด์ผ ํ๋ค.

<br>

- **movies/views.py**

  ```python
  from django.shortcuts import get_object_or_404, redirect, render
  from platformdirs import user_cache_dir
  from movies.forms import MovieForm, CommentForm
  from .models import Movie, Comment
  from django.views.decorators.http import require_safe, require_http_methods, require_POST
  from django.contrib.auth.decorators import login_required
  
  # Create your views here.
  @require_safe
  def index(request):
      movies = Movie.objects.order_by('-pk')
      context = {
          'movies': movies,
      }
      return render(request, 'movies/index.html', context)
  
  @login_required
  @require_http_methods(['GET', 'POST'])
  def create(request):
      if request.method == 'POST':
          form = MovieForm(request.POST)
          if form.is_valid():
              movie = form.save(commit=False)
              movie.user = request.user
              movie.save()
              return redirect('movies:detail', movie.pk)
      
      else:
          form = MovieForm()
      
      context = {
          'form' : form
      }
  
      return render(request, 'movies/create.html', context)
  
  @require_safe
  def detail(request, pk):
      movie = get_object_or_404(Movie, pk=pk)
      comment_form = CommentForm()
      comments = movie.comment_set.all()
  
      context = {
          'movie': movie,
          'comment_form' : comment_form,
          'comments' : comments,
      }
  
      return render(request, 'movies/detail.html', context)
  
  
  @login_required
  @require_http_methods(['GET', 'POST'])
  def update(request, pk):
      movie = get_object_or_404(Movie, pk=pk)
      if request.user == movie.user:
          if request.method == 'POST':
              form = MovieForm(request.POST, instance=movie)
              if form.is_valid():
                  movie = form.save()
                  return redirect('movies:detail', movie.pk)
      
          else:
              form = MovieForm(instance=movie)
      
      else:
          return redirect('movies:index')
  
      context = {
          'movie' : movie,
          'form' : form,
      }
  
      return render(request, 'movies/update.html', context)
  
  
  @require_POST
  def delete(request, pk):
      if request.user.is_authenticated:
          movie = get_object_or_404(Movie, pk=pk)
          if Movie.user == request.user:
              movie.delete()
      
      return redirect('movies:index')
  
  @require_POST
  def comment_create(request, pk):
      if request.user.is_authenticated:
          movie = get_object_or_404(Movie, pk=pk)
          comment_form = CommentForm(request.POST)
          if comment_form.is_valid():
              comment = comment_form.save(commit=False)
              comment.movie = movie
              comment.user = request.user
              comment.save()
          return redirect('movies:detail', movie.pk)
      return redirect('accounts:login')
  
  
  @require_POST
  def comment_delete(request, movie_pk, comment_pk):
      if request.user.is_authenticated:
          comment = get_object_or_404(Comment, pk=comment_pk)
          if request.user == comment.user:
              comment.delete()
      return redirect('movies:detail', movie_pk)
  ```

  : ํ์ด๊ฐ driver ์ญํ ์ ๋งก์ ์ด view ํจ์๊น์ง ์์ฑํ์๋๋ฐ, ๋๋ ๊ทธ ๋์ navigator๋ก์ ์๊ฒฌ ์ ์์ ์คํ ์์  ๋ฑ์ ์๊ตฌํ  ์ ์์๋ค. ๋ง์ด ์ด์ํ๊ธฐ๋ ํ์์ง๋ง, ํ์ด๊ฐ ๋๋ฌด ์ค๋ ฅ์ด ์ข์์ ๋ ๋ฐฐ์ธ ์ ์์๋ ๊ณ๊ธฐ์๋ ๊ฒ ๊ฐ๋ค. ์ด ๋น์ ๋ค์๋ ์๊ฐ์, '๋ด๊ฐ driver์๋ค๋ฉด ๋งํ์์ด ์ ์ํํ  ์ ์์์๊น'์๋ค. ๊ทธ ๋งํผ, ๊ฐ์ ์ฝ๋๋ฅผ ์์ฑํ๋๋ผ๋ ๋งํ์์ด ์ํํ๋ฉฐ, ํ์์๊ฒ ์์ ๊ฐ์ ์ค๋ค๋ ๊ฒ์ ์ค์ํ๋ค๋ ๊ฒ์ ๊นจ๋ฌ์ ์ ์์๋ค.

<br>

- **movies/forms.py**

  ```python
  from django import forms
  from .models import Movie, Comment
  
  class MovieForm(forms.ModelForm):
  
      class Meta:
          model = Movie
          exclude = ('user',)
  
  class CommentForm(forms.ModelForm):
  
      class Meta:
          model = Comment
          fields = ('content',)
  ```

  : ๋๋ ์ฌ์ค ์์ง model๊ณผ form์ ์์ฉ์ ์ ์ํํ์ง ๋ชปํ๋ค. ๋ค๋ง, ์ด ๋ถ๋ถ๋ถํฐ๋ ๋ด๊ฐ driver๊ฐ ๋์ด ์ํํ์๋๋ฐ, ์ด์  ์์ ๋ด์ฉ์ ์ฐธ๊ณ ํ  ์ ์์๋ค. ํผ์์ ํ๋ก์ ํธ๋ฅผ ์งํํ๋ ๊ฒ์ด ์๋๋ผ ๋ค๋ฅธ ๋๊ตฐ๊ฐ์ ๊ฐ์ด ์ํํ๋ค๋ณด๋, ๊ธด์ฅ๊ฐ์๊ฒ ์ฝ๋๋ฅผ ์์ฑํ๋ ๊ธฐ๋ถ์ด์๋ค. ์๋ก์ด ๋๋์ด์๊ณ , ๋์์ง ์์๋ค.

<br>

- **movies/models.py**

  ```python
  from django.db import models
  from django.conf import settings
  
  # Create your models here.
  class Movie(models.Model):
      user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
      title = models.CharField(max_length=20)
      description = models.TextField()
  
      def __str__(self):
          return self.title
  
  class Comment(models.Model):
      movie = models.ForeignKey(Movie, on_delete=models.CASCADE) 
      user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
      content = models.CharField(max_length=100)
  
      def __str__(self):
          return self.title
  ```

  : modelํํธ ๋ํ ForeignKey๋ฅผ ์์ฉํ  ์ ์์ด์ผ  ํด์ ์กฐ๊ธ ๋ฒ๋ฒ๊ฑฐ๋ฆฌ๊ธด ํ๋๋ฐ, ๊ทธ๋๋ ์ด๋ฒ ์ฃผ์ ๋ฐฐ์ ๋ ๋ด์ฉ์ ๋ ์ฌ๋ฆฌ๋ฉด์ ์ฐจ๊ทผ์ฐจ๊ทผ ํด๊ฒฐํ  ์ ์์๋ ๊ฒ ๊ฐ๋ค. ๋ช์ธ์์ ์ ํ์ง ๋๋ก ์ค๋ฅ์์ด ํด๊ฒฐํ๋ ค ํ์๊ณ , ์ด ๋๋ถํฐ ๊ธด์ฅํ์ง ์๊ณ  ์งํํ๋ค ๋ณด๋ ์ค์๋ฅผ ์ค์ผ ์ ์์๋ ๊ฒ ๊ฐ๋ค.

<br>

---

## โAfter finishing..

>   ใใใใ์ผ๊ณฑ๋ฒ์งธ ๊ดํต ํ๋ก์ ํธ๋ฅผ ์งํํ์๋ค. ์น ๊ณผ์ ์ ๊ต์ก๋ฐ๋ค ๋ณด๋ ๊ธ์์ผ๋ง๋ค ์์ ๊ดํต ํ๋ก์ ํธ๋ฅผ ์งํํ๊ฒ ๋๋๋ฐ, ์ด์  ์ ๋ง ์ผ๋ง ๋จ์ง ์์๊ตฌ๋ ์๊ฐ์ด ๋ ๋ค. ์ต์ข ํ๋ก์ ํธ๋ฅผ ์๋๊ณ  ์ด๋ ๊ฒ ์ฐ์ตํ๊ณ  ์๋ค๊ณ  ์๊ฐํ๋๋ฐ, ์์ฆ ๋๋ ์๊ฐ์ ๋ค์๊ณผ ๊ฐ๋ค. '๋ด๊ฐ ๋๊ตฐ๊ฐ์๊ฒ ํผํด๊ฐ ๋์ง ์์์ผ๋ฉด ์ข๊ฒ ๋ค.'์ด๋ค. ํ์ง๋ง, ์ ์ฐจ ์ด ์๊ฐ์ ์ค์ฌ ๋๊ฐ๋ ค๊ณ  ํ๋ค. ์๋ํ๋ฉด, ๋์ ์์ด๋์ด๋ฅผ ๋์ ๋๋ ค์์ผ๋ก ์ผ์ผ๋ฒ๋ฆฌ๊ฒ ๋๋ ์๋ ์๊ธฐ ๋๋ฌธ์ด๋ค. ๋๋ ๋ฐ๋์ ๋ถ์กฑํ ์ค๋ ฅ์ผ์ง๋ผ๋, ์ฐฝ์์ฑ์ผ๋ก ์น๋ถ๋ฅผ ๋ด๋ ค ํ๋ค. ๊ทธ๋ฌ๊ธฐ ์ํด ๋๋ ๋๋ ค์์ ์์ ๋ ์ฐ์ต์ ๋งค์ผ ํ๊ณ  ์๋ค. '๋๋ ์ถฉ๋ถํ ์ ํ๊ณ  ์๋ค.'๋ผ๊ณ  ๋๋์ธ๋ค.
>
>   ใใโ		์ค๋ ์ฒซ ํ์ด ํ๋ก์ ํธ๋ฅผ ์งํํ๋ฉด์, ๋๋ ์ ์ ์์ ์ ์ด๋ณด์๋ค. ๊ณตํต๋ ์ ์, ๋ด๊ฐ ๋ง์ด ์์ถ๋์ด ์๋ค๋ ๊ฒ์ด๋ค. ์ด๋ป๊ฒ ๋ณด๋ฉด, ๊ทธ ์ ๋ ํ๋ฆฌ์ง ์๋ค. ๊ฐ์ ๋ด์ฉ์ ๋ฐฐ์ ์ด๋ ์ถฉ๋ถํ ์ฐ์ต์ด ๋์ง ์์๊ธฐ์ ๊ทธ๋ฐ ์๊ฐ์ด ๋ค์๋ ๊ฒ์ด๋ค. ์ฐ์ต๋ง์ด ์ด๋ฐ ์๊ฐ์ ๋ฌผ๋ฆฌ์ณ ์ค ๊ฒ์ด๋ผ๋ ๊ฒ์ ์๋ค. ๋์๊ฐ์.
>
>   ใใโ		๋ง์ง๋ง์ผ๋ก ๋๋งบ๊ธฐ ์ ์, ์ฌ์ค accounts ์ฑ์ ๋ํด์ ์์ ์์ฑํ์ง ์์๋ค. ๋ค๋ง, ์ํํ๋ฉด์ ๋๋ ์ ์ ์ ์ด๋ณด๋ ค ํ๋ค. ์์ ์์ฑํ์ง ์์ ์ด์ ๋ ์์๋ด์ฉ๊ณผ ๋ณ๋ฐ ๋ค๋ฅด์ง ์์์ ์๋ค. ์ค๋ ํ๋ก์ ํธ๋ฅผ ์ํํ๋ฉด์ ์์ ๋ด์ฉ์ ๋ณต์ตํ๊ณ  ์๋ค๋ ์๊ฐ์ด ๋ค์๋ค. ์๊ณ ๋ฆฌ์ฆ์ ๋ฌธ์ ๋ฅผ ํ๋ฉด์ ์ค๋ ฅ์ด ๋๊ณ  ์๋ค๋ ๊ฒ์ ๋๊ผ๋๋ฐ, ์น ๊ณผ์ ๋ ๋ง์ด ๋ค๋ฅด์ง ์์ ๊ฒ ๊ฐ๋ค. ๊พธ์คํ๊ฒ๋ง ํ๋ฉด ์ค๋ ฅ์ ๋์ด๋  ๊ฒ ๊ฐ๋ค. ํ  ์ ์๋ค!
