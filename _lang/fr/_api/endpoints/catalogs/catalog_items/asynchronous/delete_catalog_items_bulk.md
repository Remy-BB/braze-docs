---
nav_title: "DELETE : Supprimer plusieurs produits du catalogue"
article_title: "DELETE : Supprimer plusieurs produits du catalogue"
search_tag: Endpoint
page_order: 1

layout: api_page
page_type: reference
description: "Cet article présente en détail l’endpoint Braze Supprimer plusieurs produits du catalogue."

---
{% api %}
# Supprimer plusieurs produits du catalogue
{% apimethod delete %}
/catalogs/{catalog_name}/items
{% endapimethod %}

Utilisez cet endpoint pour supprimer plusieurs produits de votre catalogue. Chaque requête peut prendre en charge jusqu’à 50 objets. Cet endpoint est asynchrone.

## Limite de débit

Cet endpoint a une limitation du débit partagée de 100 requêtes par minute entre tous les endpoints asynchrones de produits du catalogue.

## Paramètres de chemin

| Paramètre | Requis | Type de données | Description |
|---|---|---|---|
| `catalog_name` | Requis | String | Nom du catalogue. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Paramètres de demande

| Paramètre | Requis | Type de données | Description |
|---|---|---|---|
| `items` | Requis | Tableau | Un tableau qui contient certains objets Produit. Les objets Produit doivent contenir un `id` faisant référence aux produits que Braze doit supprimer. Jusqu’à 50 objets sont autorisés par requête. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Exemple de demande

```
curl --location --request DELETE 'https://rest.iad-03.braze.com/catalogs/restaurants/items' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "items": [
    {"id": "restaurant1"},
    {"id": "restaurant2"},
    {"id": "restaurant3"}
  ]
}'
```

## Réponse

Trois réponses de code de statut existent pour cet endpoint : `202`, `400` et `404`.

### Exemple de réponse réussie

Le code de statut `202` pourrait renvoyer le corps de réponse suivant.

```json
{
  "message": "success"
}
```

### Exemple de réponse échouée

Le code de statut `400` pourrait renvoyer le corps de réponse suivant. Consultez la [résolution des problèmes](#troubleshooting) pour plus d’informations concernant les erreurs que vous pourriez rencontrer.

```json
{
  "errors": [
    {
      "id": "items-missing-ids",
      "message": "There are 1 item(s) that do not have ids",
      "parameters": [],
      "parameter_values": []
    }
  ],
  "message": "Invalid Request",
}
```

## Résolution des problèmes

Le tableau suivant répertorie les erreurs renvoyées possibles et les étapes de résolution des problèmes associées.

| Erreur | Résolution des problèmes |
| --- | --- |
| `catalog-not-found` | Vérifiez que le nom du catalogue est valide. |
| `request-includes-too-many-items` | Votre requête contient trop de produits. La limite de produit par requête est de 50. |
| `invalid-ids` | Ces ID de produit peuvent uniquement inclure des lettres, des chiffres, des traits d’union et des traits de soulignement. |
| `ids-too-large` | Les ID de produit ne peuvent pas contenir plus de 250 caractères. |
| `ids-not-unique` | Vérifiez que les ID de produit dans la requête sont uniques. |
| `ids-not-strings` | Les ID de produit doivent être de type chaîne de caractères. |
| `items-missing-ids` | Il y a des produits qui n’ont pas d’ID de produit. Vérifiez que chaque produit possède un ID de produit. |
{: .reset-td-br-1 .reset-td-br-2}

{% endapi %}