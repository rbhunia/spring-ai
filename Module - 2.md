
Understanding the `PromptTemplate` Abstraction
The PromptTemplate is a cornerstone abstraction in Spring AI, enabling developers to dynamically generate prompts for Large Language Models (LLMs). Instead of hardcoding prompts directly into your application, PromptTemplate allows you to define prompts with placeholders that can be populated with data at runtime. This approach promotes code reusability, flexibility, and maintainability, making it easier to experiment with different prompts and adapt to changing requirements. This lesson will delve into the intricacies of PromptTemplate, exploring its structure, usage, and benefits.

Understanding the Core Concepts of PromptTemplate
At its heart, a PromptTemplate is a string that contains placeholders. These placeholders are identified by a specific syntax, typically using curly braces {}. When you use the PromptTemplate, you provide values for these placeholders, and the template engine replaces them with the corresponding values to create the final prompt that is sent to the LLM.

Key Components
Template String: This is the base string that defines the structure of the prompt. It includes both static text and placeholders.
Placeholders: These are the variables within the template string that will be replaced with actual values.
Input Variables: These are the names of the placeholders, which are used to map values to the correct locations in the template.
Template Engine: The underlying mechanism that performs the substitution of placeholders with values. Spring AI often leverages templating engines like FreeMarker or Thymeleaf, but it also provides a simple built-in engine.
Benefits of Using PromptTemplate
Dynamic Prompt Generation: Create prompts on the fly based on user input, data from a database, or other dynamic sources.
Code Reusability: Define a template once and reuse it with different values, avoiding code duplication.
Maintainability: Easily update and modify prompts without changing the core application logic.
Experimentation: Quickly test different prompt variations by simply changing the template or the input values.
Separation of Concerns: Decouple the prompt definition from the application logic, making the code cleaner and easier to understand.
Creating and Using PromptTemplate
Let's explore how to create and use PromptTemplate with practical examples.

Basic Example
Suppose you want to create a prompt that asks an LLM to summarize a given text. You can define a PromptTemplate like this:

import org.springframework.ai.prompt.PromptTemplate;
import org.springframework.ai.prompt.Prompt;
import java.util.Map;

public class PromptTemplateExample {

    public static void main(String[] args) {
        // 1. Define the template string with a placeholder for the text to summarize.
        String templateString = "Summarize the following text: {text}";

        // 2. Create a PromptTemplate instance with the template string.
        PromptTemplate promptTemplate = new PromptTemplate(templateString);

        // 3. Create a map to hold the values for the placeholders.
        Map<String, Object> model = Map.of("text", "The quick brown fox jumps over the lazy dog. This is a classic pangram.");

        // 4. Generate the prompt by passing the values to the PromptTemplate.
        Prompt prompt = promptTemplate.create(model);

        // 5. Print the generated prompt.
        System.out.println(prompt.toString());
    }
}
Explanation:

We define a templateString with a placeholder {text}.
We create a PromptTemplate instance using the templateString.
We create a Map called model to store the value for the text placeholder. The key in the map corresponds to the name of the placeholder in the template.
We call the create() method on the PromptTemplate instance, passing in the model map. This method replaces the placeholders in the template with the corresponding values from the map, creating a Prompt object.
Finally, we print the generated prompt to the console.
Output:

Summarize the following text: The quick brown fox jumps over the lazy dog. This is a classic pangram.
Advanced Example with Multiple Placeholders
Let's create a more complex example with multiple placeholders. Suppose you want to generate a prompt that asks an LLM to write a short story based on a given theme and character.

import org.springframework.ai.prompt.PromptTemplate;
import org.springframework.ai.prompt.Prompt;
import java.util.Map;

public class AdvancedPromptTemplateExample {

    public static void main(String[] args) {
        // 1. Define the template string with placeholders for the theme and character.
        String templateString = "Write a short story about a {character} who discovers a {theme}.";

        // 2. Create a PromptTemplate instance with the template string.
        PromptTemplate promptTemplate = new PromptTemplate(templateString);

        // 3. Create a map to hold the values for the placeholders.
        Map<String, Object> model = Map.of(
                "character", "brave knight",
                "theme", "hidden treasure"
        );

        // 4. Generate the prompt by passing the values to the PromptTemplate.
        Prompt prompt = promptTemplate.create(model);

        // 5. Print the generated prompt.
        System.out.println(prompt.toString());
    }
}
Explanation:

We define a templateString with two placeholders: {character} and {theme}.
We create a PromptTemplate instance using the templateString.
We create a Map called model to store the values for the character and theme placeholders.
We call the create() method on the PromptTemplate instance, passing in the model map.
Finally, we print the generated prompt to the console.
Output:

Write a short story about a brave knight who discovers a hidden treasure.
Using Different Data Types
The values you provide for the placeholders don't have to be strings. You can use other data types as well, such as numbers, booleans, or even more complex objects. The PromptTemplate will automatically convert these values to strings before inserting them into the prompt.

import org.springframework.ai.prompt.PromptTemplate;
import org.springframework.ai.prompt.Prompt;
import java.util.Map;

public class DataTypePromptTemplateExample {

    public static void main(String[] args) {
        // 1. Define the template string with placeholders for a name and age.
        String templateString = "Hello, my name is {name} and I am {age} years old.";

        // 2. Create a PromptTemplate instance with the template string.
        PromptTemplate promptTemplate = new PromptTemplate(templateString);

        // 3. Create a map to hold the values for the placeholders.
        Map<String, Object> model = Map.of(
                "name", "Alice",
                "age", 30
        );

        // 4. Generate the prompt by passing the values to the PromptTemplate.
        Prompt prompt = promptTemplate.create(model);

        // 5. Print the generated prompt.
        System.out.println(prompt.toString());
    }
}
Output:

Hello, my name is Alice and I am 30 years old.
Handling Missing Values
What happens if you don't provide a value for a placeholder in the model map? By default, the PromptTemplate will throw an exception. However, you can configure the template engine to handle missing values in different ways, such as by using a default value or by simply leaving the placeholder empty. This behavior depends on the underlying template engine being used.

Integrating with the Customer Support Chatbot Case Study
Recall the customer support chatbot case study introduced in Module 1. We can use PromptTemplate to dynamically generate prompts for different customer inquiries. For example, we can create a template for answering questions about product features:

import org.springframework.ai.prompt.PromptTemplate;
import org.springframework.ai.prompt.Prompt;
import java.util.Map;

public class ChatbotPromptTemplateExample {

    public static void main(String[] args) {
        // 1. Define the template string for answering product feature questions.
        String templateString = "Answer the following question about our product: {question}. The product is a customer support chatbot powered by Spring AI.";

        // 2. Create a PromptTemplate instance with the template string.
        PromptTemplate promptTemplate = new PromptTemplate(templateString);

        // 3. Get the customer's question (this would typically come from user input).
        String customerQuestion = "What are the key features of the chatbot?";

        // 4. Create a map to hold the value for the question placeholder.
        Map<String, Object> model = Map.of("question", customerQuestion);

        // 5. Generate the prompt by passing the question to the PromptTemplate.
        Prompt prompt = promptTemplate.create(model);

        // 6. Print the generated prompt (this would be sent to the LLM).
        System.out.println(prompt.toString());
    }
}
Explanation:

We define a templateString that includes the customer's question and provides context about the product.
We create a PromptTemplate instance using the templateString.
We simulate getting the customer's question from user input.
We create a Map called model to store the customer's question.
We call the create() method on the PromptTemplate instance, passing in the model map.
Finally, we print the generated prompt, which would then be sent to the LLM for processing.
This approach allows us to easily adapt the chatbot to handle different types of inquiries by creating different PromptTemplate instances for each type of question.

Exercises
Personalized Greeting: Create a PromptTemplate that generates a personalized greeting message. The template should include placeholders for the user's name and the current time of day (e.g., "Good morning, {name}!").
Story Generation: Create a PromptTemplate that generates a story prompt. The template should include placeholders for the main character, the setting, and the conflict (e.g., "Write a story about a {character} in a {setting} who faces a {conflict}.").
Product Description: Create a PromptTemplate that generates a product description. The template should include placeholders for the product name, features, and benefits (e.g., "Describe the {product} which has the following features: {features}. The main benefits are: {benefits}.").
Email Subject Line: Create a PromptTemplate that generates an email subject line. The template should include placeholders for the topic and the recipient (e.g., "Regarding {topic} for {recipient}").
Next Steps and Future Learning
Now that you understand the basics of PromptTemplate, you're well-prepared to explore more advanced prompt engineering techniques. In the next lesson, we'll delve into the ChatClient and CompletionClient interfaces, which are used to interact with LLMs and send them the prompts generated by PromptTemplate. We'll also explore how to handle the responses from the LLMs and extract the information you need. Furthermore, Module 3 will cover advanced prompt template techniques like variables, conditionals, and loops, allowing you to create even more dynamic and sophisticated prompts.
