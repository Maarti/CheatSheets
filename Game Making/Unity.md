# Unity cheatsheet

## Collider Interaction Matrix
![Collider Interaction Matrix](img/collider_interaction_matrix.png)

## Tips
  * Use [`[RuntimeInitializeOnLoadMethod]`](https://docs.unity3d.com/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html) tu run a method when game is initialized (whithout linking the script to a gameobject)
  * Activate the `Debug` mode in the top right of the inspector to display private variables
  * Generate chart in realtime i nthe inspector with:
  ```
  public AnimationCurve curve = new AnimationCurve();
  void Update() {
    curve.AddKey(Time.realtimeSinceStartup, Mathf.Sin(Time.time));
  }
  ```
  

## Optimization

### Script Optimization
  * It's more efficient to use [`gameObject.CompareTag`](https://docs.unity3d.com/ScriptReference/Component.CompareTag.html) than `==`
  
### [UI optimization](https://unity3d.com/fr/how-to/unity-ui-optimization-tips)

* **Diviser les canvas entre statiques et dynamiques**. Lorsqu'un élément du canvas change, tout le canvas est re-dessiné. [Source](https://youtu.be/_wxitgdx-UI?t=23m36s)
* Désactiver `Raycast Target` pour les éléments statiques ou non-interactifs.
