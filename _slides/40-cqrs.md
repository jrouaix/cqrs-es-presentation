# C.Q.R.S.
### Command & Query Responsibility Segregation

-----
## A Command
- Aim to change the system state
- Can be rejected due to business logic

</br>

## A Query
- Does not change the system state
- Have no business logic

Notes:
# Do not split them and you're good for bad design
 * get_latest API, that erase the latest 

---
## On a single object
```
    interface IBadIterator
    {
        (bool, object) GetNext();
    }

    interface ICqrsIterator
    {
        object Current { get; }
        bool MoveNext();
    }
```

---
## In the data layer
```
// Create, Update, Delete
interface IWriteUserRepository {
    int AddUser(User user);
    void UpdateUser(int userId, User user);
    void RemoveUser(string userId);
}

// Read
interface IReadUserRepository {
    User GetUser(int userId);
    User[] GetUsers(...search parameters...);
}
```

notes:
Do not forget pagination when you return an Array !

---
## In the business layer
```
interface IUserManager {
    int AddUser(User user);
    void MoveUser(int userId, Adress newAdress);
    void ElevateUser(int userId); // make an administrator
    void DeactivateUser(int userId);
    // ...
}

interface IUserSearchService {
    UserData GetUser(int userId);
    UserData[] GetUsers(...search parameters...);
    UserData[] GetAdminUsers(...search parameters...);
    UserData[] GetDeactivatedUsers(...search parameters...);
    bool IsUserAdmin(int userId);
    // ...
}
```

note: 
you can already see that the command/query sementics start to derive.

---
## In a database

<img src="../_assets/views.gif"/>

note:
Views
- decorelate read usage from the "real" model

---
## In a database - master / mirrors version

<img src="../_assets/7090390-screen-shot-2017-11-01-at-121854-pm.png" width="600em"/>

note:
- Write only on the master
- Read only on the mirrors

---
### multiple models ?

notes:
- what if we'd like to have multiple distinct models ? 
- one for the master/writes, one or some for the read needs ?

-----
# How to do it wrong

---
## Dual write

<img src="../_assets/dual_writes.gif" width="700em"/>

<div class="footer">
https://www.confluent.io/blog/using-logs-to-build-a-solid-data-infrastructure-or-why-dual-writes-are-a-bad-idea/
</div>

Notes:
- what if any of this writes go wrong ?
- will your system have a way to get back to consistency ?
- How the F... will this be performant ?