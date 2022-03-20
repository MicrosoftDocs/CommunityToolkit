# Contribute to the .NET MAUI Community Toolkit documentation

Thank you for your interest in contributing to the .NET MAUI Community Toolkit documentation.

Documentation is **required** when completed a proposal as part of our [proposal workflow](https://github.com/CommunityToolkit/Maui/projects). 

## Starting your changes

You will need to fork this repository. We strongly recommend that you create a branch from your `main` branch so that it will reduce any complications when submitting your Pull Request.

## Making your changes

This is where you get to add your content.

### Adding a new file

Please make sure the following changes are made:
- Include the new file in the `TOC.yml` file at the appropriate level (e.g. documentation pages for converters will go under the "Converters" name)
- Include links to the new file in any markdown files that require it (e.g. documentation pages for converters will also require that a link is added to the `converters/index.md` file, the same should be true for all specific documentation pages)
- Use the [template file](https://github.com/MicrosoftDocs/CommunityToolkit/blob/main/docs/maui/.template.md) as a starting point
- Follow the **General rules** section

### Modifying a file

This should be simpler than adding a new file:
- Follow the **General rules** section.

### General rules

- Always refer to the underlying technology as .NET MAUI and not just MAUI.
- Code examples should follow the [same guidelines](https://github.com/CommunityToolkit/Maui/blob/main/CONTRIBUTING.md#contributing-code---best-practices) as the toolkit and it's sample application.
- Keep the code examples clear and concise, only try to show the concept to the user and not lots of extra code that makes it more difficult to follow the concept.
- Links to Microsoft documentation pages should not include locale information and they should be relative e.g.
```markdown
https://docs.microsoft.com/en-gb/dotnet/maui/
```
should be shortened to:
```markdown
/dotnet/maui/
```
- Try to use a spell and grammar checker.

## Submitting changes

Once you have completed your changes make sure you push them up and then open a Pull Request.