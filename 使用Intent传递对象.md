## ʹ��Intent���ݶ���
1. Serializable��ʽ �� �򵥡�Ч�ʵ�
- Serializable�����л�����˼����ʾ��һ������ת���ɿɴ洢��ɴ����״̬��
- ���л���Ķ�������������Ͻ��д��䣬Ҳ���Դ洢�����ء�
- ���л��ķ�������һ����ȥʵ��Serializable����ӿڼ��ɡ�
```
��Person�����л���

public class Person implements Serializable {

    private String name;

    private int age;
    
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
    
}

��FirstActivity�е�д��:

Person person = new Person();
person.setName("Tom");
person.setAge(20);
Intent intent = new Intent(FirstActivity.this,SecondActivity.class);
intent.putExtra("person_data",person);
startActivity(intent);

��SecondActivity�л�ȡ�������

Perosn person = (Person) getIntent.getSerializableExtra("perosn_data");
```
2. Parcelable��ʽ ���Ƽ�ʹ��
- Parcelable��ʽʵ��ԭ���ǽ�һ�������Ķ�����зֽ⣬���ֽ���ÿһ���ֶ���Intent��֧�ֵ��������ͣ�����Ҳ��ʵ�ִ��ݶ���Ĺ����ˡ�
```
��Person��ʵ��Parcelable�ӿڣ�

public class Person implements Parcelable {

    private String name;

    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public int describeContents() {
        return 0;
    }

    @Override
    public void writeToParcel(Parcel parcel, int i) {
        parcel.writeString(name);//д��name
        parcel.writeInt(age);//д��age
    }
    
    public static final Parcelable.Creator<Person> CREATOR = new Parcelable.Creator<Person>(){

        @Override
        public Person createFromParcel(Parcel parcel) {
            Person person = new Person();
            //ע�����������˳��һ��Ҫ�͸ղ�д����˳����ȫ��ͬ
            person.name = parcel.readString();//����name
            person.age = parcel.readInt();//����age
            return person;
        }

        @Override
        public Person[] newArray(int size) {
            return new Person[size];
        }
    };
    
}

��FirstActivity�е�д��:ͬ��

��SecondActivity�л�ȡ�������

Perosn person = (Person) getIntent.getParcelableExtra("perosn_data");
```