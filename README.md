# tiny_interpretor 
tiny_interpretor 是一个使用cpp实现的简单的计算器，支持变量的设置和常见的单目双目三目和比较运算，并给出结果

计划：
增加函数定义支持和函数导入支持

# 代码片段

```
int main() 
{
    using std::string;

    auto source = std::vector<std::string>{
        string("let complex = 1.48 + + (1>2?1:2) - ( (0.4 * (3+5) < 5) + 5 + 100 ) < 3 ? 1: 2; "),
        string("let ba = complex + 3; "),
        string("ba * 2.5 + 200 * 4; "),
        string("let ba = 300; "),
        string("ba - 300 < 0.001; "),
    };

    //for(;;) {
    compiler::Parser       parser{ source };
    compiler::expression_ptr_t expr;

    try {
        for (;;) {
            if (parser.MovetoNextToken() != compiler::Parser::END) {
                expr = compiler::statement(parser);
                std::printf("%.2lf\n", expr->exec());
                //printExpression(expr);
            }
            else
                break;
        }
    }
    catch (std::runtime_error& e) {
        std::cerr << "runtime error: " << e.what() << std::endl;
    }
    catch (...) {
        std::cerr << "unexpected error " << std::endl;
    }
    //Sleep(50);
    //}
    return 0;
}
```
