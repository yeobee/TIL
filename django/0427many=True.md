```
Got AttributeError when attempting to get a value for field `content` on serializer `CommentSerializer`.
The serializer field might be named incorrectly and not match any attribute or key on the `list` instance.
Original exception text was: 'list' object has no attribute 'content'.
```

```
 many=True 넣어줘야한다
 
 get_list_or_404은 데이터 많이 옴
```

```
get_object_or_404는 데이터 하나만 불러오니깐 
 many=True가 필요없다
```

