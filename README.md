### 系统介绍

基于SpringBoot和Vue实现的电子产品销售商场采用前后端分离的架构方式，前台系统实现了用户注册/登录、首页、全部商品、优惠咨询、后台管理、在线客服、购物车、个人中心等功能模块，后台系统实现了登录、商家注册、系统首页、个人中心、用户管理、商家管理、商品类别管理、全部商品管理、系统管理、订单管理等功能模块。

### 技术选型

开发工具：idea2020.3+webstorm2020.3

运行环境：jdk1.8+mysql5.7+nodejs12.19.0

服务端技术：springboot+mybatis-plus+fastjson

前端技术：html+css+vue+axios+element-ui

### 成果展示

前台系统->注册/登录
<img width="1892" height="1031" alt="前台系统-注册登录" src="https://github.com/user-attachments/assets/4d346085-8372-4cd7-964c-8a7ca8991f4f" />

前台系统->首页
<img width="1875" height="1027" alt="前台系统-首页" src="https://github.com/user-attachments/assets/c39ebc8a-cb05-4604-810f-6f47058aab7b" />

前台系统->全部商品
<img width="1875" height="1031" alt="前台系统-全部商品" src="https://github.com/user-attachments/assets/50804dea-52fc-44bf-8d66-423953475785" />

前台系统->在线客服
<img width="1892" height="1027" alt="前台系统-在线客服" src="https://github.com/user-attachments/assets/87618d90-5bf7-4ba6-860e-01b9d15b21d1" />

前台系统->购物车
<img width="1876" height="957" alt="前台系统-购物车" src="https://github.com/user-attachments/assets/806e25a0-5ff7-4872-8c1a-f3d51b5eb219" />

前台系统->个人中心

后台系统->注册/登录 输入图片说明

后台系统->个人中心 输入图片说明

后台系统->用户管理 输入图片说明

后台系统->商家管理 输入图片说明

后台系统->商品类别管理 输入图片说明

后台系统->全部商品管理 输入图片说明

后台系统->系统管理 输入图片说明

后台系统->订单管理 输入图片说明

### 源码展示

@RestController

@RequestMapping("/orders")

public class OrdersController {

@Autowired

private OrdersService ordersService;

//查询

@RequestMapping("/query")

public R query(OrdersEntity orders){

    EntityWrapper< OrdersEntity> ew = new EntityWrapper< OrdersEntity>();
    ew.allEq(MPUtil.allEQMapPre( orders, "orders")); 
    OrdersView ordersView =  ordersService.selectView(ew);
    return R.ok("查询订单成功").put("data", ordersView);
    
}

//后端详情

@RequestMapping("/info/{id}")

public R info(@PathVariable("id") Long id){

    OrdersEntity orders = ordersService.selectById(id);
    return R.ok().put("data", orders);
    
}

//前端详情

@IgnoreAuth

@RequestMapping("/detail/{id}") 
public R detail(@PathVariable("id") Long id){ 

    OrdersEntity orders = ordersService.selectById(id); 
    return R.ok().put("data", orders);
    
}

//后端保存

@RequestMapping("/save")

public R save(@RequestBody OrdersEntity orders, HttpServletRequest request){

    orders.setId(new Date().getTime()+new Double(Math.floor(Math.random()*1000)).longValue());
    orders.setUserid((Long)request.getSession().getAttribute("userId"));
    ordersService.insert(orders);
    return R.ok();
    
}

//前端保存

@RequestMapping("/add")

public R add(@RequestBody OrdersEntity orders, HttpServletRequest request){

    orders.setId(new Date().getTime()+new Double(Math.floor(Math.random()*1000)).longValue());
    ordersService.insert(orders);
    return R.ok();
    
}

//修改

@RequestMapping("/update")

@Transactional

public R update(@RequestBody OrdersEntity orders, HttpServletRequest request){

    ordersService.updateById(orders);//全部更新
    return R.ok();
    
}

//删除

@RequestMapping("/delete")

public R delete(@RequestBody Long[] ids){

    ordersService.deleteBatchIds(Arrays.asList(ids));
    return R.ok();
    
}

}

### 账号地址及其它说明

1、地址说明

前台系统：localhost:8081

后台系统：localhost:8082

2、账号说明

用户：zhazha/123456

商家：dataonlinecom/123456

管理员：admin/admin

3、目录结构展示

输入图片说明

4、项目结构展示

输入图片说明

5、运行步骤

1）创建数据库、导入sql脚本

2）修改application.yml中的数据库配置文件，启动服务端

3）分别在front和admin目录下打开cmd，执行npm install下载依赖

4）下载完毕后启动前端npm run serve，访问端口

### 获取方式(可远程调试)

访问链接(在浏览器中手动输入下图中的地址)：

输入图片说明

若资源获取失败，可添加happy35596339(vx)或1204901965(qq)进行交流
