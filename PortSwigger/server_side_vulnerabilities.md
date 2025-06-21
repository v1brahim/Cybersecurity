## Path Traversal
### Lets you access any directory by using ../../../ to go back to home directory
### This can be dangerous if we can access some sensitive files such as /etc/passwd

### Lab Solution
```bash
GET /image?filename=../../../../../../../etc/passwd HTTP/2
```

## Access Control
### Vertical Privelage Escalation
### When a normal user gain access to functionality they are not allowed to access

## Lab 1 Solution
```bash
Look at /robots.txt u will find admin panel, browse to admin panel
```

## Lab 2 Solution
### After browsing through the source code we find an admin function that discloses admin directory
```javascript
var isAdmin = false;
if (isAdmin) {
   var topLinksTag = document.getElementsByClassName("top-links")[0];
   var adminPanelTag = document.createElement('a');
   adminPanelTag.setAttribute('href', '/admin-7ey9aw');
   adminPanelTag.innerText = 'Admin panel';
   topLinksTag.append(adminPanelTag);
   var pTag = document.createElement('p');
   pTag.innerText = '|';
   topLinksTag.appendChild(pTag);
}
```
## Parameter-based access control methods
 Some applications determine the user's access rights or role at login, and then store this information in a user-controllable location. This could be:

    A hidden field.
    A cookie.
    A preset query string parameter.

The application makes access control decisions based on the submitted value. For example:
```bash
https://insecure-website.com/login/home.jsp?admin=true
https://insecure-website.com/login/home.jsp?role=1
```
This approach is insecure because a user can modify the value and access functionality they're not authorized to, such as administrative functions. 

## Lab 3 Solution
### Frist we login with the credentials given
### After we login we can capture any activity we preform using the normal user
### for exammple in this case we can reset our gmail
### After capturing the action with burpsuite we find a paramter called Admin set to False
```
POST /admin HTTP/2
Host: 0a2100af039b86b3800612b300df00e8.web-security-academy.net
Cookie: session=CeC2SKdpdnyio6cj27ZreGfd0kjQOCEt; Admin=True
```
### We can Simply set its value to true and preform the delete carlos user action to solve the lab
```
POST /admin/delete?username=carlos HTTP/2
```
## Horizontal Privelage Escalation
 Horizontal privilege escalation occurs if a user is able to gain access to resources belonging to another user, instead of their own resources of that type. For example, if an employee can access the records of other employees as well as their own, then this is horizontal privilege escalation.

Horizontal privilege escalation attacks may use similar types of exploit methods to vertical privilege escalation. For example, a user might access their own account page using the following URL:
https://insecure-website.com/myaccount?id=123

If an attacker modifies the id parameter value to that of another user, they might gain access to another user's account page, and the associated data and functions.
Note

This is an example of an insecure direct object reference (IDOR) vulnerability. This type of vulnerability arises where user-controller parameter values are used to access resources or functions directly.

In some applications, the exploitable parameter does not have a predictable value. For example, instead of an incrementing number, an application might use globally unique identifiers (GUIDs) to identify users. This may prevent an attacker from guessing or predicting another user's identifier. However, the GUIDs belonging to other users might be disclosed elsewhere in the application where users are referenced, such as user messages or reviews. 


