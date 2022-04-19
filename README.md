# 📌 My Seventh Project 📋

---

##### - Outline : 2022년 4월 8일, 일곱번째 관통 프로젝트를 수행하였다. 한 주 전까지만 해도 오랜만에 수행하는 프로젝트라서 서투르게 수행했는데, 오늘은 그래도 수월하게 수행할 수 있었다. 사실, 그 배경에는 다른 이유가 존재한다. 오늘부터 프로젝트는 페어프로젝트로 이루어졌고, 오로지 협동심만이 프로젝트를 완벽하게 수행할 수 있게 해준다는 것을 느낄 수 있었기 때문이다. 나의 페어는 같은 반의 '전상현' 학우였다. 평소에도 침착하게 문제 해결을 하는 것을 잘 알고 있었으며, 몇 번 나에게 도움을 주었던 학우여서 고마운 마음을 가지고 본 프로젝트에 집중하려고 하였다. 중간 중간 쉬는 시간을 조율할 수도 있어서 좋았던 것 같고, 큰 오류없이 프로젝트를 마칠 수 있었다. 마치고 나서는 내가 부족하면 팀원이 같이 고생한다는 것을 또 한 번 느낄 수 있었던 것 같으며, 그랬기에 다음 페어를 위해서도 내가 다음 주도 열심히 공부해야 한다고 생각이 들었다. 자, 이제 오늘의 프로젝트를 수행하면서 느꼈던 점과 개선해야 할 점을 중심으로 README 파일을 작성해보려 한다.

---

<br>


# **< Title : "사용자 인증기반 관계형 DB 설계" >**

*(This project was carried out in **Python 3.9.9 and Django 3.2.12 environment .**)*

- *요구사항 : 이는 커뮤니티 서비스의 게시판 기능 개발을 위한 단계로, 해당 기능들은 향후 커뮤니티 서비스의 필수 기능으로 사용될 것이라고 한다. 명세서에 기술되어 있는 사항들은 필수적으로 구현해야 한다.*

---

*(프로젝트 파일의 settings.py, urls.py와 base.html 등의 기본 설정은 제외하고 , 앱 파일에 관해서만 작성합니다.)*

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
  
  : url을 입력하였을 때, 혹은 해당url로의 이동을 지정해 줄 때에 올바른 view 함수가 실행될 수 있도록 설정해 주었다. 이를 작성하면서 오류 사항은 없었다. 다만, 마지막 줄인 movie_pk와 comment_pk를 응용해야 할 때에는 페어와 함께 많은 고민을 해야 했다.

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

  : 페어가 driver 역할을 맡아 이 view 함수까지 작성하였는데, 나는 그 때에 navigator로서 의견 제시와 오타 수정 등을 요구할 수 있었다. 많이 어색하기도 하였지만, 페어가 너무 실력이 좋아서 더 배울 수 있었던 계기였던 것 같다. 이 당시 들었던 생각은, '내가 driver였다면 막힘없이 잘 수행할 수 있었을까'였다. 그 만큼, 같은 코드를 작성하더라도 막힘없이 수행하며, 팀원에게 안정감을 준다는 것은 중요하다는 것을 깨달을 수 있었다.

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

  : 나는 사실 아직 model과 form의 응용을 잘 수행하지 못한다. 다만, 이 부분부터는 내가 driver가 되어 수행하였는데, 이전 수업 내용을 참고할 수 있었다. 혼자서 프로젝트를 진행하는 것이 아니라 다른 누군가와 같이 수행하다보니, 긴장감있게 코드를 작성하는 기분이었다. 새로운 느낌이었고, 나쁘진 않았다.

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

  : model파트 또한 ForeignKey를 응용할 수 있어야  해서 조금 버벅거리긴 했는데, 그래도 이번 주에 배웠던 내용을 떠올리면서 차근차근 해결할 수 있었던 것 같다. 명세서에 적혀진 대로 오류없이 해결하려 하였고, 이 때부터 긴장하지 않고 진행하다 보니 실수를 줄일 수 있었던 것 같다.

<br>

---

## ✏After finishing..

>   　　　　일곱번째 관통 프로젝트를 진행하였다. 웹 과정을 교육받다 보니 금요일마다 작은 관통 프로젝트를 진행하게 되는데, 이제 정말 얼마 남지 않았구나 생각이 든다. 최종 프로젝트를 앞두고 이렇게 연습하고 있다고 생각하는데, 요즘 드는 생각은 다음과 같다. '내가 누군가에게 피해가 되지 않았으면 좋겠다.'이다. 하지만, 점차 이 생각을 줄여 나가려고 한다. 왜냐하면, 나의 아이디어를 나의 두려움으로 삼켜버리게 놔둘 수는 없기 때문이다. 나는 반드시 부족한 실력일지라도, 창의성으로 승부를 내려 한다. 그러기 위해 나는 두려움을 없애는 연습을 매일 하고 있다. '나는 충분히 잘 하고 있다.'라고 되뇌인다.
>
>   　　​		오늘 첫 페어 프로젝트를 진행하면서, 느낀 점을 위에 적어보았다. 공통된 점은, 내가 많이 위축되어 있다는 것이다. 어떻게 보면, 그 점도 틀리진 않다. 같은 내용을 배웠어도 충분한 연습이 되지 않았기에 그런 생각이 들었던 것이다. 연습만이 이런 생각을 물리쳐 줄 것이라는 것을 안다. 나아가자.
>
>   　　​		마지막으로 끝맺기 전에, 사실 accounts 앱에 대해서 위에 작성하진 않았다. 다만, 수행하면서 느낀 점을 적어보려 한다. 위에 작성하지 않은 이유는 수업내용과 별반 다르지 않아서 였다. 오늘 프로젝트를 수행하면서 수업 내용을 복습하고 있다는 생각이 들었다. 알고리즘은 문제를 풀면서 실력이 늘고 있다는 것을 느꼈는데, 웹 과정도 많이 다르진 않은 것 같다. 꾸준하게만 하면 실력은 늘어날 것 같다. 할 수 있다!
