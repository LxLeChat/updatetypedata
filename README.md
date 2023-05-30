##we can add a type to a pscutomobject after it's creation ( for example if you convertfrom-json, but cannot cast into a type )
```powershell
update-TypeData -MemberType ScriptMethod -MemberName tutu -Value {return $this.a} -TypeName somecustomType
$a=convertfrom-json -InputObject '{"a":1}'
$a.psobject.TypeNames.Insert(0,"somecustomType")
$a.tutu()
```

# updatetypedata
Way faster when creating custom object, to use update-typedata then add-member on each newly created pscustomobject

```powershell
$T1 = @{
    TypeName = "MyCustomType"
    MemberType = "ScriptMethod"
    MemberName = "GetSometing"
    Value = {
          return $this.name
        }
    }
}

$T1 = @{
    TypeName = "MyCustomType"
    MemberType = "ScriptMethod"
    MemberName = "GetOtherStuff"
    Value = {
          return $this.plop
        }
    }
}

Update-TypeData @T1
Update-TypeData @T2

$plop = [pscustomobject]@{
        PSTypeName = "MyCustomType"
        Name = "Toto
        plop = 1
    }
    
$Plop | gm
```
