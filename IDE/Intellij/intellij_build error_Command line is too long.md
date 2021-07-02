### Command line is too long... 해결법



프로젝트 폴더 > .idea > workspace.xml



`PropertiesComponent`에 아래 property를 추가해준다.

```xml
  <component name="PropertiesComponent">
    <property name="dynamic.classpath" value="true" />
  </component>
```

