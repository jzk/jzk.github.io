title: Camel里各种常用对象在不同语境下的调用方式
date: 2015-07-08 01:59:31
categories:
- Dev
tags:
- Camel
---

来总结一下property，header和body在各个context下的引用方式

## property (defined in routeGroup)   

**definition**    
```
<property name="orderAmountMultiplier" value="100" />
```

**groovy**      

```
camelContext.resolvePropertyPlaceholders('{{x.x.x}}')
```
  
**simple**      

```
{{x.x.x}}
```

**uri reference**   

```
<to uri="{{x.x.x}}"/>

```

<!--more-->

**java**
```
#TODO
```

_The syntax to use Camel's property placeholder is to use `\{{key}}` for example `{{file.uri}}` where file.uri is the property key. More detail info can be found [here](http://camel.apache.org/using-propertyplaceholder.html)_

## property in Camel
**definition**         
```
<setProperty propertyName="xx">
   <simple>{{x.x.x}}</simple>
</setProperty>
```
**groovy**      
```
exchange.properties.xx
```

**simple**      
```
${property.xx}
```

**uri reference**   
```
<log message="bla bla ${property.xx}"/>
```

**java**
```
#TODO
```

## header in Camel
**definition**

```
<setHeader headerName="xx">
    <constant>SELECT name, id FROM store.store</constant>
</setHeader>
```

**groovy**        
```
request.headers.xx
```

**simple**       
```
$simple{header.xx}
```

**uri reference** 
```
#deducable, need prove
```

**java**
```
#TODO
```

## body in Camel
**definition**       
```
<property name="xx" value="100" /> 
```

**groovy**        
```
request.body
```

**simple**      
```
${body['xx']}/${body.xx}
```

**uri reference**    
```
#deducable, need prove
```

**Java**                    
```
exchange.getIn().setBody()
```

