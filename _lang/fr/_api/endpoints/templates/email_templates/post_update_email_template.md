---
nav_title: "POST : Mettre à jour le modèle d’e-mail"
article_title: "POST : Mettre à jour les modèles d’e-mail"
search_tag: Endpoint
page_order: 4
layout: api_page
page_type: reference
description: "Cet article présente en détail l’endpoint Braze Mettre à jour les modèles d’e-mail."

---
{% api %}
# Mettre à jour les modèles d’e-mail existants
{% apimethod post %}
/templates/email/update
{% endapimethod %}

Utilisez cet endpoint pour mettre à jour des modèles d’e-mail sur le tableau de bord de Braze. Vous pouvez accéder à un `email_template_id` de modèle d’e-mail en allant sur la page **Templates & Media (Modèles et médias)**. L’[endpoint Créer un modèle d’e-mail]({{site.baseurl}}/api/endpoints/templates/email_templates/post_create_email_template/) renvoie également une référence `email_template_id`.

Tous les champs autres que l’`email_template_id` sont facultatifs, mais vous devez spécifier au moins un champ à mettre à jour.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#afb25494-3350-458d-932d-5bf4220049fa {% endapiref %}

## Limite de débit

{% multi_lang_include rate_limits.md endpoint='default' %}

## Corps de la demande

```
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
```

```json
{
  "email_template_id": (required, string) your email template's API Identifier,
  "template_name": (optional, string) the name of your email template,
  "subject": (optional, string) the email template subject line,
  "body": (optional, string) the email template body that may include HTML,
  "plaintext_body": (optional, string) a plaintext version of the email template body,
  "preheader": (optional, string) the email preheader used to generate previews in some clients,
  "tags": (optional, array of Strings) tags must already exist,
  "should_inline_css": (optional, Boolean) one of 'true' or 'false' is expected
}
```

## Paramètres de demande

| Paramètre | Requis | Type de données | Description |
| --------- | ---------| --------- | ----------- |
|`email_template_id`| Requis |String|Votre [identifiant API du modèle d’e-mail]({{site.baseurl}}/api/identifier_types/).|
|`template_name`|Optional|String|Nom de votre modèle d’e-mail.|
|`subject`|Optional|String|Ligne Objet du modèle d’e-mail.|
|`body`|Optional|String|Corps du modèle d’e-mail pouvant inclure du HTML.|
|`plaintext_body`|Optional|String|Une version en texte brut du corps du modèle d’e-mail.|
|`preheader`|Optional|String|Accroche d’e-mail utilisé pour générer des aperçus chez certains clients.|
|`tags`|Optional|String|[Tags]({{site.baseurl}}/user_guide/administrative/app_settings/manage_app_group/tags/) doit déjà exister.|
|`should_inline_css`|Optional|Boolean|Active ou désactive la fonction `inline_css` par modèle. Si non renseigné, Braze utilisera le paramètre par défaut de l’AppGroup. `true` ou `false` est attendu.|
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
```
curl --location --request POST 'https://rest.iad-01.braze.com/templates/email/update' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "email_template_id": "email_template_id",
  "template_name": "Weekly Newsletter",
  "subject": "This Week'\''s Styles",
  "body": "Check out this week'\''s digital lookbook to inspire your outfits. Take a look at https://www.braze.com/",
  "plaintext_body": "This is the updated text within my email body and here is a link to https://www.braze.com/.",
  "preheader": "We want you to have the best looks this Summer",
  "tags": ["Tag1", "Tag2"]
}'
```

## Erreurs possibles

Le tableau suivant répertorie les erreurs renvoyées possibles et les étapes de résolution des problèmes associées, le cas échéant.

| Erreur | Résolution des problèmes |
| --- | --- |
| Le nom du modèle est obligatoire | Saisissez un nom de modèle. |
| Les balises doivent être un tableau | Les balises doivent être un tableau de chaînes de caractères, par exemple `["marketing", "promotional", "transactional"]`. |
| Toutes les balises doivent être des chaînes de caractères | Assurez-vous que vos balises sont comprises entre des guillemets (`""`). |
| Certaines balises sont introuvables | Pour ajouter une balise lors de la création d’un modèle d’e-mail, la balise doit déjà exister dans Braze. |
| Valeur non valide pour `should_inline_css`. `true` ou `false` était attendu | Ce paramètre accepte uniquement les valeurs booléennes true ou false). Assurez-vous que la valeur de `should_inline_css` n’est pas comprise entre des guillemets (`""`), sinon la valeur est envoyée comme chaîne de caractères. |
{: .reset-td-br-1 .reset-td-br-2}

{% endapi %}
