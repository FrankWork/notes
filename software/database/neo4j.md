# 创建

```sql
CREATE (<node-name>:<label-name>)

CREATE (emp:Employee)
CREATE (dept:Dept)

CREATE (
   <node-name>:<label-name>
   { 	
      <Property1-name>:<Property1-Value>
      ........
      <Propertyn-name>:<Propertyn-Value>
   }
)

CREATE (dept:Dept { deptno:10,dname:"Accounting",location:"Hyderabad" })
CREATE (emp:Employee{id:123,name:"Lokesh",sal:35000,deptno:10})


CREATE (
    <node-name>:<label-name1>:<label-name2>.....:<label-namen>
)

CREATE (m:Movie:Cinema:Film:Picture)
```

# 检索

```sql
MATCH 
(
   <node-name>:<label-name>
)

MATCH (dept:Dept)

RETURN 
   <node-name>.<property1-name>,
   ........
   <node-name>.<propertyn-name>

RETURN dept.deptno


MATCH (dept: Dept) RETURN dept.deptno,dept.dname
MATCH (dept: Dept) RETURN dept // 显式图状结构
```

```sql
CREATE (e:Customer{id:"1001",name:"Abc",dob:"01/10/1982"})
CREATE (cc:CreditCard{id:"5001",number:"1234567890",cvv:"888",expiredate:"20/17"})
MATCH (e:Customer) RETURN e.id,e.name,e.dob
```

# 关系

```sql
CREATE (<node1-name>:<label1-name>)-
	[(<relationship-name>:<relationship-label-name>)]
	->(<node2-name>:<label2-name>)

CREATE (p1:Profile1)-[r1:LIKES]->(p2:Profile2)
```


# Where

```sql
WHERE <condition>
WHERE <condition> <boolean-operator> <condition>

<condition>: <property-name> <comparison-operator> <value>


MATCH (emp:Employee) WHERE emp.name = 'Abc' RETURN emp
MATCH (emp:Employee) WHERE emp.name = 'Abc' OR emp.name = 'Xyz' RETURN emp


MATCH (<node1-label-name>:<node1-name>),(<node2-label-name>:<node2-name>) 
WHERE <condition>
CREATE (<node1-label-name>)-[<relationship-label-name>:<relationship-name>
       {<relationship-properties>}]->(<node2-label-name>)

OPTIONAL MATCH (e:Customer),(cc:CreditCard) 
WHERE e.id = "1001" AND cc.id= "5001" 
CREATE (e)-[r:DO_SHOPPING_WITH{shopdate:"12/12/2014",price:55000}]->(cc) 
RETURN r
```


# SET, order by, union, limit, skip

```SQL
MATCH (dc:DebitCard) SET dc.atm_pin = 3456 RETURN dc

MATCH (emp:Employee) RETURN emp.empid,emp.name,emp.salary,emp.deptno ORDER BY emp.name 
MATCH (emp:Employee) RETURN emp.empid,emp.name,emp.salary,emp.deptno ORDER BY emp.name DESC

<MATCH Command1>
   UNION
<MATCH Command2>


MATCH (cc:CreditCard) RETURN cc.id as id,cc.number as number,cc.name as name,
UNION
MATCH (dc:DebitCard) RETURN dc.id as id,dc.number as number,dc.name as name,

MATCH (emp:Employee) RETURN emp LIMIT 2
MATCH (emp:Employee) RETURN emp SKIP 2
```


# merge

```sql
MERGE (<node-name>:<label-name>
{
   <Property1-name>:<Pro<rty1-Value>
   .....
   <Propertyn-name>:<Propertyn-Value>
})


CREATE (book:Book {id:122,title:"Neo4j Tutorial",pages:340,price:250}) 
MATCH (book : Book) RETURN book
MATCH (book { id:122 }) REMOVE book.price RETURN book
MATCH (e: Employee) DELETE e

MATCH (cc:CreditCard)-[r]-(c:Customer)RETURN r 
MATCH (cc:CreditCard)-[r]-(c:Customer)RETURN cc, r, c 

```



