Как мы знаем, ингресс - это тот тип объектов кубернетес, который требует для своей работы стороннего ингресс контроллера. И если мы создадим ингресс, без контроллера он работать не будет.  

Давайте с вами поставим ингресс-контроллер. Сделаем это с помощью утилиты helm. Мы не будем детально рассматривать то, как работает эта утилита, главное, что что нам важно, что ингресс контроллер будет установлен в неймспейс kube-system. 

Итак **запускаем две команды**

Теперь дождемся, когда ингресс-контроллер реально запустится. Для этого запустим в цикле команду, которая из всех *подов* `kube-system`, отфильтрует *под* ингресс контроллера по меткам `app.kubernetes.io/name` и `app.kubernetes.io/component`. 

**Запускаем команду.**

Ждем пока *под* ингресс контроллера не окажется в статусе Running. 

И выходим из цикла сочетанием клавиш Ctrl-C.

Ингресс-контроллер в данном случае - это nginx и контроллер, который читает изменения сущности Ingress. Nginx внутри Kubernetes запущен, как обычное приложение, и для него также есть Service. Тип сервиса LoadBalancer, т.е. доступ к nginx можно получить вне кластера по внешнему IP адресу.  

Посмотрим настройки этого сервиса.

**Запускаем команду** kubectl describe.

Как видим, это обычный сервис. 

Сохраним значение внешнего IP в переменную окружения `NGINX_EXTERNAL_IP`.

**Запускаем команду.** 

Теперь **сделаем запрос** с помощью команды curl.

Т.к. созданных ингрессов еще нет, то nginx отдает стандартную 404ую ошибку. 

Итак, мы с вами установили ингресс контроллер, и научились делать к нему запросы.