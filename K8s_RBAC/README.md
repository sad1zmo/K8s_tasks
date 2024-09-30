# K8s_RBAC

## Задание:

- Создайте неймспейс с именем test-rbac.
- Создайте сервис-аккаунт с именем test-user в namespace test-rbac и токен.
- Создайте сервис-аккаунт с именем test-admin в namespace test-rbac и токен.
В namespace test-rbac создайте роль test-role с правами:
На serviceaccounts все возможные права, кроме удалений.
На pods – get, list, watch.
Не должен иметь права на создание/изменение rolebindings в данном неймпсейсе.
- Создайте rolebinding с именем test-binding и привяжите роль test-role к serviceaccount test-user в неймспейсе test-rbac.
- В namespace test-rbac cоздайте binding с именем admin-binding для serviceaccount test-admin таким образом, чтобы он получил права на все ресурсы в текущем неймспейсе. Используйте clusterrole: cluster-admin.
- Добавьте в текущий kubeconfig нового пользователя (serviceaccount test-user ) и контекст с именем sa-context . Проверьте доступ через команду kubectl --context sa-context -n test-rbac get sa.

## Решение:

- В units.yaml описаны все сущности необходимые для задания.
- Что бы запустить все сущности необходимо выполнить команду: `kubectl apply -f units.yaml`.
- далее на необходимо получить токены с помощью команды: `kubectl -n test-rbac get secret test-user -o jsonpath="{.data.token}" | base64 --decode`
- полученный токен необходимо добавить в kubeconfig (в нашем случае нашего пользователя test-user) пример как сдлеать находится в файле config.
- конфиг файл обычно находится по пути: ~/.kube/config

## Проверка:

```
kubectl --context sa-context -n test-rbac get sa
```

- Если все нормально получите список сервис аккаунтов.