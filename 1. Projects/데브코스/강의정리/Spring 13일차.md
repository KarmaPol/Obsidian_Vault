## 타임리프
#### 반복문 예시
```html
<tr th:each="customer: ${customers}" th:object="${customer}" >
  <td th:text="${customer.customerId}"></td>
  <td th:text="*{name}"></td>
  <td th:text="*{email}"></td>
  <td th:text="*{createdAt}"></td>
  <td th:text="*{lastLoginAt}"></td>
</tr>
```
#### Form 예시
```html
<form th:action="@{/customers/new}" method="post">
  <div class="mb-3">
    <label for="exampleInputEmail1" class="form-label">Email address</label>
    <input type="email" name="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
  </div>
  <div class="mb-3">
    <label for="exampleInputPassword1" class="form-label">Name</label>
    <input type="text" name="name" class="form-control" id="exampleInputPassword1">
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>
</form>
```
## WebApplicationContext
ServletContext 생성 시 ApplicationContext도 생성
Controller 계층은 ServletApplicationContext
서비스 계층, 데이터 엑세스 계층은 RootApplicationContext로 분리
-> 모놀로틱 어플리케이션은 ServletApplicationContext 하나만 생성하기도 한다

https://jaehun2841.github.io/2018/10/21/2018-10-21-spring-context/#Web-Application-Context

