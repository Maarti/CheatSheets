# Unity cheatsheet

## Collider Interqction Matrix
![Collider Interqction Matrix](img/collider_interaction_matrix.png)

## Tips
  * Use [[RuntimeInitializeOnLoadMethod]](https://docs.unity3d.com/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html) tu run a method when game is initialized (whithout linking the script to a gameobject)
  * It's more efficient to use [CompareTag](https://docs.unity3d.com/ScriptReference/Component.CompareTag.html) than `==`

## Optimization

### [UI optimization](https://unity3d.com/fr/how-to/unity-ui-optimization-tips)

* **Diviser les canvas entre statiques et dynamiques**. Lorsqu'un élément du canvas change, tout le canvas est re-dessiné. [Source](https://youtu.be/_wxitgdx-UI?t=23m36s)
* Désactiver `Raycast Target` pour les éléments statiques ou non-interactifs.