# UnityHealthBar
This is a starter kit for a health bar system in Unity.

##Importing to Your Project
Simply open your Unity project, and then double-click the package file (HealthBarStarterPack.unitypackage).  
A popup will appear in Unity to prompt you - click "Import", and all the needed files will be inside your project.

##Example
To view the example, drag the TestEnemy (HealthBarStarterPack/Prefabs/TestEnemy) prefab into your scene.  
When you press Play, a HealthBar should spawn above it. When you hold SpaceBar down, it should get damaged gradually, and the health bar should reflect that!

##Using the Health System
The Health class is lightweight and simple to use. To use it, attach it to the GameObject you want it on.  
The Health system must be initialized with ```Initialize(float maxHealthAmount)```.  
To deal damage, call ```Damage (float amount)```.

##Using the BarUI System with Health System
1) Drag and drop the HealthBar prefab into your scene  
2) Attach the HealthBar gameObject from (1) onto the gameObject you want (i.e Player)  
3) Attach the Health script onto the same gameObject from (2)  
4) Inside the master script of the gameObject (e.g Player), add this chunk to ```Start()``` (or Initialize() if you made your own)  
(Please change the value inside `Initialize(100f)` to whatever Health amount you want)
```
    health = transform.GetComponent<Health> ();  
    health.Initialize (100f);  
    BarUI barUi = GameObject.Instantiate(healthBarPrefab, transform).GetComponent<BarUI> ();  
    barUi.transform.localPosition = new Vector3 (0f, .4f, 0f);  
    barUi.Initialize (health);
```

###Using BarUI on Other Things
If you wish to use this on other systems (e.g Mana Systems), follow these steps:  
1) Ensure your new class inherits from `ObservableRatio` class (i.e `public class ManaSystem : ObservableRatio`)  
2) Override `GetRatio()` by making a new method in the class,  
i.e `public override float GetRatio() { //calculate ratio here }`  
3) Drag HealthBar to your gameObject, and rename it accordingly (i.e ManaSystem)  
4) Ensure that the BarUI in HealthBar gets initialized to observe your class. Here is an example, for a class `ManaSystem`, with the HealthBar gameObject renamed to ManaBar
```
    manaSystem = transform.GetComponent<ManaSystem> ();  
    manaSystem.Initialize (100f);  
    BarUI barUi = transform.Find("ManaBar").GetComponent<BarUI> ();  
    barUi.Initialize (manaSystem);
```
