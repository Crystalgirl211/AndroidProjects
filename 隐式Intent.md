Intent��ʽ������
- ��绰��
```java
    Intent intent = new Intent(Intent.ACTION_CALL);
    intent.setData(Uri.parse("tel:10086"));
    startActivity(intent);
```
- ���ţ�
```java
    Intent intent = new Intent(Intent.ACTION_DIAL);
    intent.setData(Uri.parse("tel:10086"));
    startActivity(intent);
```
