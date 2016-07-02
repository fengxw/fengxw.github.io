---
title:  Symfony 搭建RESTful API 项目
author: fengxw
---

Symfony 是一系列可复用的PHP组件结合的Web后台框架，可以通过引用不同的bundle来构建我们的项目。其中最流行的就是构建RESTful API。

---

1. 安装[lnmp](http://www.lnmp.org/)环境或[vagrant](https://www.vagrantup.com)开发环境

2. 下载最新的[symfony安装包](https://symfony.com/download)

    ```
    	sudo curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony
    	sudo chmod a+x /usr/local/bin/symfony 
    	symfony new project
    ```
    
3. 下载最新[composer安装包](http://www.phpcomposer.com/)

    ```
    curl -sS https://getcomposer.org/installer | php
    mv composer.phar /usr/local/bin/composer
    ```
    
4. 安装相关bundle

* FOSRestBundle 
           - `composer require friendsofsymfony/rest-bundle`（网络不好时，可以先在composer.json文件中添加 `"friendsofsymfony/rest-bundle": "^1.7", `然后运行`composer update nothing`, 再运行`composer install`）

           - 在app/AppKernel.php file中添加 `new FOS\RestBundle\FOSRestBundle(),`

           - 在app/config/config.yml->framework 启用serializer属性

           ```
            serializer:
                enable_annotations:true
            ```
            
           - 在app/config/config.yml添加如下配置
           
           ```
            fos_rest:
                body_converter:
                    enabled: true
                view:
                    view_response_listener: 'force'
                    formats:
                        json: true
                format_listener:
                    rules:
                        - { path: ^/api, priorities: [ json ], fallback_format: json, prefer_extension: true }
                        - { path: '^/', priorities: [ 'html', '*/*'], fallback_format: html, prefer_extension: true }
            ```
            
           - 在app/config/routing.yml设置prefix，例子如下：

            ```
            clash_api:
                resource: "@ClashApiBundle/Resources/config/routing.yml"
                prefix:   /api
            ```   
            
* JMSSerializerBundle 
        - `composer require jms/serializer`（网络不好时，可以先在composer.json文件中添加 `"jms/serializer-bundle": "^1.0", `然后运行`composer update nothing`, 在运行`composer install`）
            
        - 在app/AppKernel.php file中添加 `new JMS\SerializerBundle\JMSSerializerBundle(),`

            
5. 创建rest风格的class时，`use FOS\RestBundle\Controller\FOSRestController; `继承 FOSRestController, 例子如下：
    ```
    class PostController extends FOSRestController
    {
        // code something here .....
    }
    ```

6. 声明rest api的几种方式：
 * `use FOS\RestBundle\Controller\Annotations; `在function的上方添加注释，例子如下：
    ```   
    /**
     * @Annotations\Get("/posts/category/{id}")
     */
    public function getPostsByCategoryAction() 
    {
        // code something here .....
    }
    ```
  * 当直接通过id获取对象时，也可以省略不写，例子如下：
    ```
    public function getPostAction(Post $post)
    {
        // code something here .....
    }
    ```
    
7. 返回json view的几种方式：
    * GET 方法通过查询直接获取对象时，可以通过系列化的方式，返回特定的字段。
        - 现在entity中设置好需要返回的字段

        ```
        /**
         * @ORM\Entity()
         */
        class Post
        {
            /**
             * @var int
             *
             * @ORM\Id
             * @ORM\Column(type="integer")
             * @ORM\GeneratedValue
             * @Serializer\Groups({"ManyPosts"})
             */
            private $id;
        
            /**
             * @Serializer\Groups({"ManyPosts"})
             * @Serializer\VirtualProperty
             * @Serializer\SerializedName("owner")
             */
            public function degenerateOwner()
            {
                return [
                    'id' => $this->user->getId(),
                    'username' => $this->user->getUsername(),
                    'picture_id' => $this->user->getPictureId(),
                ];
            }
        }
        ```
        
        - 在对应的class里 `use FOS\RestBundle\View\View;` 在function的上方添加注释，例子如下：

        ```
        /**
         * @Annotations\View(serializerGroups={"Default", "ManyPosts"})
         */
        public function getPostsOwnerAction()
        {
            // code something here .....
            return $posts;
        }
        ```
        
* POST/PUT/PATCH等方法返回自定义view时，不用注释，在return构建自定义view，例子如下：

    ```
    return $this->handleView(
        new View(
            array(
                'id' => $post->getId(),
            ),
            Response::HTTP_CREATED
        )
    );
    ```
