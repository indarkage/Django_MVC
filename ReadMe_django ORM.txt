1.	Создать двух пользователей (с помощью метода User.objects.create_user).
>>> user1 = User.objects.create(username='James', first_name='Bond')
>>> user2 = User.objects.create(username='Jack', first_name='Reacher')
2.	Создать два объекта модели Author, связанные с пользователями.
>>> Author.objects.create(AuthorUser=user1)
>>> Author.objects.create(AuthorUser=user2)
3.	Добавить 4 категории в модель Category.
>>> Category.objects.create(name='Sport')
>>> Category.objects.create(name='Books')
>>> Category.objects.create(name='Travel')
>>> Category.objects.create(name='Criminal')
4.	Добавить 2 статьи и 1 новость.
>>> Post.objects.create(author=Author.objects.get(AuthorUser=User.objects.get(username='Jack')), categoryType='AR', title = 'TITLE11', text='TEXT11')
>>> Post.objects.create(author=Author.objects.get(AuthorUser=User.objects.get(username='Jack')), categoryType='AR', title = 'TITLE22', text='TEXT22')
>>> Post.objects.create(author=Author.objects.get(AuthorUser=User.objects.get(username='James')), categoryType='NW', title = 'TITLE1', text='TEXT1')
5.	Присвоить им категории (как минимум в одной статье/новости должно быть не меньше 2 категорий).
>>> Post.objects.get(pk=4).postCategory.add(Category.objects.get(name='Sport'))
>>> Post.objects.get(pk=5).postCategory.add(Category.objects.get(name='Books')) 
>>> Post.objects.get(pk=5).postCategory.add(Category.objects.get(name='Travel')) 
>>> Post.objects.get(pk=6).postCategory.add(Category.objects.get(name='Criminal'))

6.	Создать как минимум 4 комментария к разным объектам модели Post (в каждом объекте должен быть как минимум один комментарий).
>>> Comment.objects.create(commentUser=User.objects.get(username='James'), commentPost = Post.objects.get(pk=4), text='COMMENT TEXT1') 
>>> Comment.objects.create(commentUser=User.objects.get(username='James'), commentPost = Post.objects.get(pk=5), text='COMMENT TEXT1') 
>>> Comment.objects.create(commentUser=User.objects.get(username='James'), commentPost = Post.objects.get(pk=6), text='COMMENT TEXT1') 
>>> Comment.objects.create(commentUser=User.objects.get(username='Jack'), commentPost = Post.objects.get(pk=4), text='COMMENT TEXT2')  
>>> Comment.objects.create(commentUser=User.objects.get(username='Jack'), commentPost = Post.objects.get(pk=5), text='COMMENT TEXT2') 
>>> Comment.objects.create(commentUser=User.objects.get(username='Jack'), commentPost = Post.objects.get(pk=6), text='COMMENT TEXT2') 
7.	Применяя функции like() и dislike() к статьям/новостям и комментариям, скорректировать рейтинги этих объектов.
>>> Post.objects.get(pk=4).like()
>>> Post.objects.get(pk=5).like() 
>>> Post.objects.get(pk=6).dislike() 
>>> Comment.objects.get(pk=4).like()
>>> Comment.objects.get(pk=5).like()  
>>> Comment.objects.get(pk=6).dislike()
8.	Обновить рейтинги пользователей.
>>> Author.objects.get(AuthorUser=User.objects.get(username="James")).update_rating()
>>> Author.objects.get(AuthorUser=User.objects.get(username="Jack")).update_rating()  
9.	Вывести username и рейтинг лучшего пользователя (применяя сортировку и возвращая поля первого объекта).
>>> Author.objects.all().order_by('-RatingAuthor').values('AuthorUser', 'RatingAuthor')[0]  
>>> User.objects.get(pk=3)
10.	Вывести дату добавления, username автора, рейтинг, заголовок и превью лучшей статьи, основываясь на лайках/дислайках к этой статье.
>>> Post.objects.all().order_by('-rating').values('dateCreation', 'author', 'rating', 'title', 'text')[0]
11.	Вывести все комментарии (дата, пользователь, рейтинг, текст) к этой статье.
>>> Comment.objects.all().order_by('-rating').values('dateCreation', 'commentUser', 'rating', 'text')[0]   
