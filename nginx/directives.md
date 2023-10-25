```
location /test {
    default_type text/html;
    return 200 '[$args] [$arg_type]';
}
```

- `$args` ? 이후로 작성된 모든 Url Params를 출력한다.
- `$arg_type` type 이라는 KEY 를 갖는 Url Param 의 값을 출력한다.
  
