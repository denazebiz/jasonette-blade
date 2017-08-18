# Jasonette with Blade
Jasonette (http://jasonette.com/) it's a wondeful tool for making native apps using only json. I think it's more similar to making websites than creating a json response for an API Rest. So why not use the same tools available for websites and apply them to jasonette?.

This is an example of what you could get using a template engine like Laravel's Blade. All the benefits of a template engine (include, inheritance, comments, functions) with the wonders of jasonette united.

```
{
  "$jason": {
    "head": {
      @include('common.head.title', ['value' => 'Login']),
      @include('common.head.offline'),
      "styles": {
        @include('app.class.input')
      }
    },
    "body": {
      "style": {
        @include('common.style.border.none'),
        @include('app.background.image')
      },
      "header": {
        {{--@include('common.properties.title', ['value' => 'Header Title']),--}}
        "style": {
          @include('common.style.color.black'),
          @include('common.style.background.transparent')
        }
      },
      "sections": [
        {
          "items": [
            @include('common.items.space', ['height' => 10]),
            {
              @include('common.components.image'),
              @include('common.properties.url', 
                ['value' => url('/img/logo.png')]),
              "style": {
                @include('common.style.align.center'),
                @include('common.style.width', ['value' => 200])
              }
            },
            @include('common.items.space', ['height' => 50]),
            {
              @include('common.layouts.horizontal'),
              "components": [
                @include('common.items.space'),
                {
                  @include('common.components.textfield'),
                  @include('common.properties.name', ['value' => 'username']),
                  @include('common.properties.placeholder', ['value' => 'User']),
                  @include('common.properties.class', ['value' => 'input'])
                },
                @include('common.items.space')
              ]
            },
            {
              @include('common.layouts.horizontal'),
              "components": [
                @include('common.items.space'),
                {
                  @include('common.components.textfield'),
                  @include('common.properties.name', ['value' => 'password']),
                  @include('common.properties.placeholder', ['value' => 'Password']),
                  @include('common.properties.class', ['value' => 'input']),
                  "style": {
                    @include('common.style.secure')
                  }
                },
                @include('common.items.space')
              ]
            },
            @include('common.items.space', ['height' => 5]),
            {
              @include('common.layouts.horizontal'),
              "components": [
                @include('common.items.space'),
                {
                  @include('common.components.button'),
                  @include('common.properties.text', ['value' => 'LOGIN']),
                  "style": {
                    @include('common.style.width.full'),
                    @include('common.style.align.center'),
                    @include('common.style.font.helveticaneue.bold'),
                    @include('common.style.size', ['value' => 12]),
                    @include('common.style.padding', ['value' => 10]),
                    @include('common.style.height', ['value' => 60]),
                    @include('app.background.red'),
                    @include('common.style.color.white')
                  },
                  "action": {
                    @include('common.action.network.request'),
                    "options": {
                      @include('common.properties.url',
                        ['value' => 'http://example.com/logInUser.php']),
                      @include('common.action.network.method.post'),
                      "data": {
                        "user": "@{{$get.username}}",
                        "password": "@{{$get.password}}"
                      }
                    },
                    "success": {
                      @include('common.action.session.set'),
                      "options" : {
                        @include('common.properties.domain', ['value' => $root]),
                        "header" : {
                          "X-User-Name" : "@{{$jason.data.user.name}}",
                          "X-Authorization" : "@{{$jason.data.token}}"
                        }
                      },
                      "success": {
                        @include('common.action.href'),
                        "options" : {
                          @include('common.properties.url', ['value' => url('/home')]),
                          @include('common.action.href.transition.replace')
                        }
                      }
                    },
                    "error": {
                      @include('common.util.banner'),
                      "options": {
                        @include('common.util.banner.types.error'),
                        @include('common.properties.title', ['value' => 'Error']),
                        @include('common.properties.description', 
                        ['value' => 'Wrong credentials.'])
                      }
                    }
                  }
                },
                @include('common.items.space')
              ]
            }
          ]
        }
      ]
    }
  }
}
```

Made with <i class="fa fa-heart">&#9829;</i> by <a href="http://ninjas.cl" target="_blank">Ninjas.cl</a>.
