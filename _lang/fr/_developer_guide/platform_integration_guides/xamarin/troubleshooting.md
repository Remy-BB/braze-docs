---
nav_title: Résolution des problèmes
article_title: Résolution des problèmes de Xamarin
platform: 
  - Xamarin
  - iOS
  - Android
page_order: 6
description: "Cet article couvre la résolution des problèmes sur iOS et Android pour la plateforme Xamarin."

---

# Résolution des problèmes

## Android

### La notification push n’apparaît pas après la fermeture de l’application à l’aide du commutateur de tâche

Si vous constatez que les notifications push n’apparaissent plus après la fermeture de l’application à l’aide du commutateur de tâche, votre application est probablement en mode Débogage. Xamarin ajoute des échafaudages en mode Débogage qui empêchent les applications de recevoir une notification push après que leur processus est tué. Si vous exécutez votre application en mode Libérer, vous devriez voir vos notifications push, même après la fermeture de l’application à l’aide du commutateur de tâche.

### Le générateur de notifications personnalisées n’est pas correctement configuré

Les générateurs de notifications personnalisées (et tous les délégués) doivent étendre [`Java.Lang.Object`][2] pour fonctionner correctement par-dessus le fossé entre C# et Java. Consultez [Xamarin][1] pour plus d’informations concernant l’implémentation d’interfaces Java.

[1]: https://developer.xamarin.com/guides/android/advanced_topics/java_integration_overview/working_with_jni/#Implementing_Interfaces
[2]: https://developer.xamarin.com/api/type/Android.Runtime.IJavaObject/