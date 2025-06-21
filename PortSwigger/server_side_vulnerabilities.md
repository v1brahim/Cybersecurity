# 1. Path Traversal

Lets you access any directory by using ../../../ to go back to home directory
This can be dangerous if we can access some sensitive files such as /etc/passwd

### Lab Solution

```bash
GET /image?filename=../../../../../../../etc/passwd HTTP/2
```



# 2. Access Control

### Vertical Privelage Escalation

When a normal user gain access to functionality they are not allowed to access

### Lab 1 Solution

```bash
Look at /robots.txt u will find admin panel, browse to admin panel
```

### Lab 2 Solution

After browsing through the source code we find an admin function that discloses admin directory

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

### Lab 3 Solution

Frist we login with the credentials given

After we login we can capture any activity we preform using the normal user

for exammple in this case we can reset our gmail

After capturing the action with burpsuite we find a paramter called Admin set to False

```
POST /admin HTTP/2
Host: 0a2100af039b86b3800612b300df00e8.web-security-academy.net
Cookie: session=CeC2SKdpdnyio6cj27ZreGfd0kjQOCEt; Admin=True
```

We can Simply set its value to true and preform the delete carlos user action to solve the lab

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

### Lab 4 Solution

We first login in with the credentials given

We find that each user has a unique GUID

After looking through some posts on the website, we find a post by our target user "carlos", and after clicking on carlos, we find that it discloses the GUID of carlos, which can be used to login as carlos and find the Solution

We login to this guid with this link

```
https://0a340040049e06d7800ab236008900a7.web-security-academy.net/my-account?id=a4a5e1f1-99e5-43e0-81d0-ce42f11bbe6a
```

#### Horizontal to vertical privilege escalation

Often, a horizontal privilege escalation attack can be turned into a vertical privilege escalation, by compromising a more privileged user. 
For example, a horizontal escalation might allow an attacker to reset or capture the password belonging to another user. If the attacker targets an administrative user and compromises their account, then they can gain administrative access and so perform vertical privilege escalation.

An attacker might be able to gain access to another user's account page using the parameter tampering technique already described for horizontal privilege escalation:

`https://insecure-website.com/myaccount?id=456`

If the target user is an application administrator, then the attacker will gain access to an administrative account page. This page might disclose the administrator's password or provide a means of changing it, or might provide direct access to privileged functionality.

### Lab 5 Solution

First we login with the given credentials to the lab website
When we go to the my-account page, we see that our user has a password hidden with javascript

We can easily go to the sourcecode and reveal the current password

We also see that our page has a parameter "?id=wiener"
The idea is to change the use wiener to "administrator", that lets us access the admin account configuration page and reveal the password for administrator

which we ca use then to delete carlos and solve the lab

## 

# 3. Authentication vulnerabilities

Conceptually, authentication vulnerabilities are easy to understand. However, they are usually critical because of the clear relationship between authentication and security.

Authentication vulnerabilities can allow attackers to gain access to sensitive data and functionality. They also expose additional attack surface for further exploits. For this reason, it's important to learn how to identify and exploit authentication vulnerabilities, and how to bypass common protection measures.

In this section, we explain:

- The most common authentication mechanisms used by websites.

- Potential vulnerabilities in these mechanisms.

- Inherent vulnerabilities in different authentication mechanisms.

- Typical vulnerabilities that are introduced by their improper implementation.

- How you can make your own authentication mechanisms as robust as possible.




