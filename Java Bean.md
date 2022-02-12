# Java Bean –

A Java Bean follows a certain standard:  
- bean should be srializable
- bean should have setters & getters
- bean should have a public no-arg constructor

Sample code:  

```java
public class User implements java.io.Serializable {

    // Properties.
    private Long id;
    private String name;
    private Date birthdate;

    // Getters.
    public Long getId() { return id; }
    public String getName() { return name; }
    public Date getBirthdate() { return birthdate; }

    // Setters.
    public void setId(Long id) { this.id = id; }
    public void setName(String name) { this.name = name; }
    public void setBirthdate(Date birthdate) { this.birthdate = birthdate; }

    // Important java.lang.Object overrides.
    public boolean equals(Object other) {
        return (other instanceof User) && (id != null) ? id.equals(((User) other).id) : (other == this);
    }
    public int hashCode() {
        return (id != null) ? (getClass().hashCode() + id.hashCode()) : super.hashCode();
    }
    public String toString() {
        return String.format("User[id=%d,name=%s,birthdate=%d]", id, name, birthdate);
    }
}
```

Advantage:  
1. Reusable software components
2. The JavaBean properties and methods can be exposed to another application

Downside:  
1. JavaBeans are mutable. So, it can't take advantages of immutable objects.
2. Creating the setter and getter method for each property separately may lead to the boilerplate code.


Reference: 
1. https://stackoverflow.com/a/1729230/6842300

