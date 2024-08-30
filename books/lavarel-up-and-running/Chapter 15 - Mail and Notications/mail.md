<!-- @format -->

# Mail

Laravel’s mail functionality is a convenience layer on top of Symfony Mailer

- you’ll set your authentication information in **config/services.php**

## Basic “Mailable” Mail Usage

Every mail message you’ll send in a modern Laravel app will be an instance of a specific PHP class, created to represent each email, called a `mailable`.

- To make a mailable, use the make:mail Artisan command:

```php
php artisan make:mail AssignmentCreated
```

```php
use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Mail\Mailable;
use Illuminate\Mail\Mailables\Content;
use Illuminate\Mail\Mailables\Envelope;
use Illuminate\Queue\SerializesModels;
class AssignmentCreated extends Mailable
{
    use Queueable, SerializesModels;
    /**
     * Create a new message instance.
     */
    public function __construct()
    {
    //
    }
    /**
     * Get the message envelope.
     */
    public function envelope(): Envelope
    {
        return new Envelope(
            subject: 'New assignment from ' . $this->trainer->name,
            from: new Address($this->trainer->email, $this->trainer->name),
        );
    }
    /**
     * Get the message content definition.
     */
    public function content(): Content
    {
        return new Content(
            view: ''emails.assignment-created',
        );
    }
    /**
     * Get the attachments for the message.
     *
     * @return array<int, \Illuminate\Mail\Mailables\Attachment>
     */
    public function attachments(): array
    {
        return [];
    }
}
```

- this class imports the `Queueable` trait for queuing your mail
- also imports the `SerializesModels` trait to serialize any Eloquent models you pass to the constructor.

### How it Works

- The class constructor is the place where you’ll pass in any data, **any properties you set as public on your mailable class will be available to the template**.
- In the `envelope()` method, you’ll set configuration details about the mail—sender, subject, metadata.
- In the `content()` method, you’ll define the content—which view you’re using to render, any Markdown contents, and text parameters
- And if you want to attach any files to the mail, you’ll use the `attachments()` method.
